---
ID: 1631
post_title: >
  How To Generate SNARK Parameters
  Securely
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/snark-parameters/
published: true
post_date: 2016-02-29 00:00:00
---
<p>There are a lot of cryptographic challenges to making a fully secure and reliable open financial system.</p>
<p>Our current top priority in the Zcash development process is to securely generate “SNARK public parameters”.</p>
<div class="section" id="what-s-the-problem">
<h2>What's the problem?</h2>
<p>The simple way to generate “SNARK public parameters” also produces a kind of cryptographic “toxic waste” which makes Zcash counterfeitable. Here’s our plan to prevent counterfeiting.</p>
<p>SNARKs — a very efficient form of Zero-Knowledge Proofs — are a cryptographic building block in Zcash. They are what allow Zcash miners to validate transactions and reject invalid transactions without disclosing any private information about the content of the transactions to those miners.</p>
<p>SNARKs require something called “the public parameters”. The SNARK public parameters are numbers with a specific cryptographic structure that are known to all of the participants in the system. They are baked into the protocol and the software from the beginning.</p>
<p>The obvious way to construct SNARK public parameters is just to have someone generate a public/private keypair, similar to an ECDSA keypair <a class="footnote-reference" href="#id2" id="id1">[*]</a>, and then destroy the private key.</p>
<p>The problem is that private key. Anybody who gets a copy of it can use it to counterfeit money. (However, it cannot violate any user’s privacy — the privacy of transactions is not at risk from this.)</p>
<p>Mitigating this threat is currently our top priority in the Zcash development process. We call the private key material “the toxic waste byproduct” — something that is produced as an unwanted side-effect of the public parameter generation, and that we need to contain and destroy as safely as possible.</p>
</div>
<div class="section" id="what-can-we-do-about-it">
<h2>What can we do about it?</h2>
<p>We’ve devised a <em>secure multiparty computation</em> in which multiple people each generate a “shard” of the public/private keypair, then they each destroy their shard of the toxic waste private key, and then they all bring together their shards of the public key to to form the SNARK public parameters. If that process works — i.e. if <em>at least one</em> of the participants successfully destroys their private key shard — then the toxic waste byproduct never comes into existence at all.</p>
<p>We wrote <a class="reference external" href="http://diyhpl.us/~bryan/papers2/bitcoin/snarks/Secure%20sampling%20of%20public%20parameters%20for%20succinct%20zero%20knowledge%20proofs.pdf">a paper on the cryptographic science</a> behind that process, which we presented at the IEEE “Oakland” Security and Privacy conference in 2015.</p>
<p>We're working on the engineering and operational details of how to implement that secure multiparty computation, using a set of well-known, trusted people to serve as the participants. We're also exploring whether there are other applications of SNARKs outside of Zcash that have the same need for public parameters, because we could generate the public parameters for those other applications at the same time as we do for Zcash.</p>
</div>
<div class="section" id="what-else-can-we-do">
<h2>What else can we do?</h2>
<p>So does this fix the problem? We think this solution is good enough to move ahead with. It completely eliminates the toxic waste private key if it works, and it would be extremely difficult for any adversary to defeat it.</p>
<p>Unfortunately there is no way to confirm, after the fact, that it actually worked. It will always be possible to worry that all N out of N of the participants may have secretly colluded together to share their private key shards, or that all N out of N participants may have had their computers compromised by an adversary who stole all of the private key shards.</p>
<p>Therefore, we're also exploring long-range ideas which — if they work out — could further mitigate this risk and other risks like it.</p>
<ul class="simple"><li>Perhaps we could leverage the modern <a class="reference external" href="https://en.wikipedia.org/wiki/Trusted_execution_environment">“Trusted Execution Environments”</a> like Intel SGX and ARM TrustZone so that even if a participant — or a compromised computer that the participant is using — tries to extract their shard of the private key, they can’t. Perhaps we could make it so that some participants use Intel SGX, others use ARM TrustZone, and others use neither, so that even if Intel SGX <em>and</em> ARM TrustZone were both compromised, the attacker would still fail to create the toxic waste byproduct because at least one of the other participants successfully destroyed their shard of it.</li>
<li>Perhaps there could be a way to repeatedly <em>extend</em> the SNARK public parameters with newly generated public key shards made by new participants, so that an attacker would fail unless they exploited not only all of the original participants but all of the new participants as well.</li>
<li>Perhaps there could be a way to audit the size of the Zcash monetary base, without compromising the privacy of any users. That way, people could at least say “Well, we can't be 100% sure that someone didn't steal the toxic waste private key, but at least we can tell that they have not (yet) used it to counterfeit money.”.</li>
<li>Perhaps there could be a new form of SNARK which has public parameters unrelated to any toxic waste private key. Nobody knows for sure if such a thing is possible, but scientists, including some of those from our team, are continuing to <a class="reference external" href="http://eprint.iacr.org/2016/116">actively investigate</a> the boundaries of what kinds of proof systems are possible.</li>
</ul></div>
<div class="section" id="the-bottom-line">
<h2>The Bottom Line</h2>
<p>There’s a kind of “cryptographic toxic waste”, which if it were to be created and exploited, would allow the attacker to counterfeit currency (although it wouldn’t allow them to violate anyone’s privacy). Our plan to prevent that uses a <em>secure multiparty computation</em> in which a set of well-known people each contribute, in such a way that if <em>any one of them</em> successfully destroys their shard, then the cryptographic toxic waste can never come into existence. We’re also working on other potential long-term defenses against risks like this.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none"><colgroup><col class="label"/><col/></colgroup><tbody valign="top"><tr><td class="label"><a class="fn-backref" href="#id1">[*]</a></td><td>I'm totally oversimplifying here. SNARK public parameters are not just an ECDSA public key — they're more like a set of a million ECDSA public keys, each of which contains an encoding of a specific wire in the SNARK circuit. But that doesn't matter for the point of this blog post.</td></tr></tbody></table></div>