---
ID: 1561
post_title: >
  Fixing Vulnerabilities in the Zcash
  Protocol
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/fixing-zcash-vulns/
published: true
post_date: 2016-04-26 00:00:00
---
<h2 style="margin-bottom:0;">Intro</h2>
by Zooko

I've worked in cryptography, information security, and digital money for half of my life (20 years, but who's counting?), and I've never worked on a cryptosystem as ambitious as Zcash. Fortunately, I've also never worked with a <a class="reference external" href="https://z.cash/team.html">team</a> so uniquely skilled at the exacting task of constructing secure and practical cryptosystems.

An essential part of the practice of computer security is an “adversarial” process in which you try to attack a system — to find weaknesses in it — at the same time as you are trying to strengthen it. This process can be disconcerting to outsiders, but to computer security experts, if we see someone finding, fixing, and publishing security issues, this gives us confidence that the system is getting stronger.

Members of our team have previously done this sort of security auditing work for others, including <a class="reference external" href="https://leastauthority.com/blog/least_authority_performs_security_audit_for_cryptocat.html">Cryptocat</a>, <a class="reference external" href="https://leastauthority.com/blog/least_authority_performs_security_audit_for_globaleaks.html">GlobaLeaks</a>, <a class="reference external" href="https://leastauthority.com/blog/least_authority_performs_security_audit_for_spideroak.html">SpiderOak</a>, and <a class="reference external" href="https://leastauthority.com/blog/least_authority_performs_incentive_analysis_for_ethereum.html">Ethereum</a>.

In this blog post, we report on the security issues we've found in the Zcash protocol while preparing to deploy it as an open, permissionless financial system.

Some of our team published the <a class="reference external" href="http://zerocash-project.org/media/pdf/zerocash-extended-20140518.pdf">original Zerocash science paper</a>, with scientific peer review, in 2014. Recently, we have extended and improved the protocol, written a detailed new <a class="reference external" href="https://github.com/zcash/zips/raw/master/protocol/protocol.pdf">protocol specification</a>, and scoured it for security vulnerabilities.

To date, we've found and fixed three security vulnerabilities:
<ol class="arabic simple">
 	<li>Zooko Wilcox found the <a class="reference external" href="https://github.com/zcash/zcash/issues/98">Faerie Gold vulnerability</a>, which would have made it possible to fool a Zcash user into thinking they received a bunch of spendable notes. In fact, when they try to spend the notes they will find that only one of them can be spent.</li>
 	<li>Taylor Hornby found the <a class="reference external" href="https://github.com/zcash/zcash/issues/738">InternalH Collision vulnerability</a>, which would let someone double-spend a specially-crafted note, if they have a computer powerful enough to find 128-bit hash collisions.</li>
 	<li>Daira Hopwood found a non-exploitable <a class="reference external" href="https://github.com/zcash/zcash/issues/836">mistake in the security proof</a>, where if one of the pseudorandom functions the protocol uses is not also collision-resistant, then notes sent to a specially-crafted private address could be double spent. (This was not exploitable because the function that is actually used does happen to be collision-resistant.)</li>
</ol>
Here is Taylor's write-up of the most impactful of these three — the InternalH Collision Vulnerability, which he found.

— Zooko Wilcox, 2016-04-25

<h2 style="margin-bottom:0;">The InternalH Collision Vulnerability</h2>
by Taylor

Had we launched Zcash without finding and fixing the InternalH Collision vulnerability, it could have been exploited to counterfeit currency. Someone with enough computing power to find 128-bit hash collisions would have been able to double-spend money to themselves, creating Zcash out of thin air.

Finding 128-bit hash collisions requires :math:`2^{64}` <a href="http://people.scs.carleton.ca/~paulv/papers/JoC97.pdf">parallelizable</a> operations, which is within reach of attackers today, so the vulnerability would have been exploitable in practice. Let's see how the attack works, and what we did to fix it.
<h3>The Mistake</h3>
The weakness was in the commitment scheme for notes. Commitment schemes are useful cryptographic tools because they let you publish a <em>commitment</em> to some information without revealing it. Then, at some later time, you can <em>open</em> the commitment to reveal the information and prove to everyone that it's the same information you committed to in the first place.

In order for this to work, commitment schemes need to satisfy two properties:
<ol class="arabic simple">
 	<li><em>Hiding</em>: You don't learn anything about the information from seeing the commitment. Even if you're pretty sure of what the information was, you shouldn't be able to confirm your guess.</li>
 	<li><em>Binding</em>: If you commit to some value, you shouldn't be able to change your mind later and say you actually committed to a different value. A commitment should <em>open</em> to one unique value, and it shouldn't be possible to open the commitment to any other value.</li>
</ol>
In Zcash, the fundamental object of value is called a “note”, which consists of the values :math:`(a_{pk}, v, ρ, r)` which have special meanings in the protocol. As part of the protocol, commitments to notes are published onto the blockchain. Here's how that commitment was computed in the original design:

:math:`InternalH = \text{SHA256Compress}(a_{pk} \text{ \| } ρ) \text{ truncated to 128 bits }`
:math:`k = \text{SHA256Compress}(r \text{ \| } InternalH)`
:math:`cm = \text{SHA256Compress}(k \text{ \| } [0]^{192} \text{ \| } v)`

Here, SHA256Compress is the compression function used internally by the SHA256 hash function.

The InternalH Collision vulnerability exists because this scheme is missing the <em>binding</em> property. It's possible to commit to one note and then open the commitment later to a different note.

It's easy to see how this can be done if you can collide 128-bit hashes. The commitment starts out by computing :math:`InternalH`, an 128-bit hash of :math:`a_{pk}` and :math:`ρ`, and then committing to that hash. If you find an
InternalH collision, then you have two different :math:`a_{pk}` and :math:`ρ` pairs :math:`(a_{pk}, ρ)` and :math:`(a_{pk}\prime, ρ\prime)` that give the same :math:`InternalH`, and you'll be able to open the commitment to either of :math:`(a_{pk}, v, ρ, r)` or :math:`(a_{pk}\prime, v, ρ\prime, r)`. So the commitment scheme isn't binding. How does this weakness translate into an attack?
<h3>The Attack</h3>
Commitments to all notes in existence are stored on the blockchain. In order to spend a note, you must prove in zero-knowledge that you know the spending key for a note that was committed to on the blockchain and you must reveal that note's nullifier. The nullifier is a value that's supposed to be unique for each note. To make sure no note can be spent twice, all nodes on the network check that they haven't seen the newly-revealed nullifier before.

The nullifier of a note :math:`(a_{pk}, v, ρ, r)` owned by a spending key :math:`a_{sk}` is computed by applying a psuedorandom function to :math:`ρ`, i.e. the nullifier is :math:`PRF_{a_{sk}}^{nf}(ρ)`. The spender must prove in zero-knowledge (without revealing :math:`ρ` or :math:`a_{sk}`) that they computed the nullifier correctly.

The InternalH weakness lets an attacker craft a note commitment for which two different valid :math:`ρ` values exist. They can find :math:`ρ_1` and a different :math:`ρ_2` such that the commitment opens to either :math:`(a_{pk}, v, ρ_1, r)` or :math:`(a_{pk}, v, ρ_2, r)`. The attacker can spend the note commitment a first time using :math:`ρ_1` revealing the nullifier :math:`PRF_{a_{sk}}^{nf}(ρ_1)`, and then spend it a second time using :math:`ρ_2` revealing the nullifier :math:`PRF_{a_{sk}}^{nf}(ρ_2)`. In effect, this note has two different nullifiers instead of just one, so it can be spent twice. Since all of this is done in zero knowledge, none of the nodes on the network can tell that both spends are referencing the same note commitment. Another variant of the attack works by finding two different :math:`a_{pk}`, rather than two different ρ.

For every 128-bit hash collision the attacker finds, they can effectively double their wealth by combining all of their Zcash into one double-spendable note and then double-spending it to themselves. So even though the :math:`2^64` operations to find a collision aren't cheap, the attack quickly pays off.
<h3>The Fix</h3>
If you read Section 5.1 of the <a class="reference external" href="http://zerocash-project.org/media/pdf/zerocash-extended-20140518.pdf">original Zerocash science paper</a>, you'll find that :math:`InternalH` was chosen to be 128 bits in order to give the commitment scheme a very strong property called <em>statistical hiding</em>. The ordinary hiding property is computational: it says that you can't learn anything about the input unless you have an absurdly fast computer (i.e. capable of breaking SHA256). Statistical hiding says that <em>even if you have an infinitely fast computer</em>, you still can't learn anything about the input. This would have allowed Zcash to retain its privacy guarantees even if one day the SHA256 hash function were broken.

To fix the vulnerability, we switched to a different commitment scheme that has secure binding. In order to keep the Zcash zero-knowledge proofs efficient to compute, we dropped the powerful statistical hiding property and settled for the regular one. This shouldn't matter in practice, since in order to break the hiding property of our new commitment scheme, you'd have to break a well-studied security property of SHA256, which seems unlikely to happen anytime soon. Here's our current design for the note commitment scheme:

:math:`cm = \text{SHA256}(\text{0xB0} \text{ \| } a_{pk} \text{ \| } v \text{ \| } ρ \text{ \| } r)`

<h3>Conclusion</h3>
Building secure crypto protocols is hard, and even our team of world-class cryptographers and security engineers will make mistakes along the way. Despite the challenge, we're optimistic that our practices of careful security review and transparency will lead to a secure product.

At this point the Zcash protocol has been subjected to intense security review, first through scientific peer review, and then by our in-house team of experts. But we need even <em>more</em> scrutiny to gain assurance that the protocol is safe.

If you like the challenge of hunting for bugs in crypto protocols, we would love it if you had a look over our <a class="reference external" href="https://github.com/zcash/zips/raw/master/protocol/protocol.pdf">protocol specification</a>. If you can break our protocol and tell us how you did it, you will be helping all of humanity to gain an open, permissionless, privacy-preserving financial system!

— Taylor Hornby with Zooko Wilcox, 2016-04-25