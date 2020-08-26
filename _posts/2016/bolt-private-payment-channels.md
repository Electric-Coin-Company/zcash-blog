---
ID: 4871
post_title: 'BOLT: Private Payment Channels'
post_name: bolt-private-payment-channels
post_date: 2016-08-01 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/bolt-private-payment-channels/
published: true
tags:
  - bitcoin
  - BOLT
  - privacy
categories:
  - General
---
<p>Matthew Green and I have written a paper introducing BOLT (Blind Off-chain Lightweight Transactions), which offers a fast, private payment channel protocol inspired by the Lightning Network. We believe that this will make Zcash more scalable and practical, while maintaining its strong privacy protections.</p>
<p>TL;DR: Using BOLT, multiple payments on the same channel cannot be linked together, even by colluding parties. Payments occur in milliseconds and do not require block confirmation. All a merchant learns is that he is being paid on some channel he has open. Payments can be routed via third parties, avoiding the need for a customer and merchant to directly have a channel, while maintaining privacy against malicious third parties by both keeping the participants anonymous (even if the third party colludes), and hiding the value transferred. All of this requires that the channel be funded with private funds, otherwise malicious parties can violate your privacy by forcing channel closure. A pre-print of the paper can be found at <a class="reference external" href="http://eprint.iacr.org/2016/701">http://eprint.iacr.org/2016/701</a>.</p>
<div class="section" id="the-problem">
<h2>The Problem</h2>
<p>Blockchain-based cryptocurrencies work by recording every transaction in public on a blockchain. This has the distinct advantage of eliminating the need for trusted parties. But it has serious privacy, scalability, and latency problems because <em>you are recording every transaction in public on a blockchain</em>. You need the space to record every transaction in the blockchain (see the whole Bitcoin block size debate), recording the transaction in a block takes minutes, and of course the recording is public, so people can figure out a lot about what you are doing.</p>
</div>
<div class="section" id="payment-channels">
<h2>Payment channels</h2>
<p>Payment channel protocols, such as the Lightning Network, address the scale and latency issues by using the blockchain only to escrow funds and resolve disputes. Other than that, users exchange what are essentially blockchain-enforced IOUs, which aren’t recorded on the blockchain unless there is a dispute.</p>
<p>How does this work? Alice and Bob both agree to an initial IOU splitting funds they put in the channel (e.g. they each put in $50 and the IOU is Alice: $50, Bob: $50). This money is held in escrow on the blockchain and released only by a valid IOU signed by both Alice and Bob. For Alice to pay Bob $5, she verifiably destroys her old IOU, and she and Bob sign a new IOU “Alice: $45, Bob: $55.” They can do this repeatedly until either party wants to cash out. At this point, either Alice or Bob can post the latest IOU to the blockchain (or both can post, in the event of a dispute). Thus only channel opening and closure are recorded on the blockchain.</p>
</div>
<div class="section" id="channels-are-not-private">
<h2>Channels are not private</h2>
<p>Channel opening and closure leaves a record identifying the customer, merchant, and the initial and final split of funds. These are often the very things that must be hidden.</p>
<p>Suppose Tor (or another anonymity service) took micropayments to pay for bandwidth. Effectively,  every webpage Alice views via Tor  would require a micropayment via a payment channel, at say a tenth-of-a-cent per page view. If we can see that Alice has a payment channel with Tor for $1.00 that closes with a zero balance every month, then we know she is a heavy Tor user. If Alice is an activist or a journalist, this may bring her to the attention of the authorities as someone with “something to hide”  even if she is careful to only use Tor from coffee shops or the like. And If Alice lives in e.g. Turkey, that might be a very bad idea.</p>
<p>Fortunately, this is exactly the sort of problem that Zcash was designed to solve. By using Zcash instead of an all-transparent ledger like Bitcoin or Ethereum, the blockchain no longer contains information linking channel opening and closure back to Alice. But Zcash only handles privacy for on-chain payments; it does not deal with the IOUs.</p>
<p>The problem is these IOUs form a unique identifier which can be used to track Alice much like a cookie.  Anyone who observes these (e.g. the Tor exit node) will not <em>a priori</em> know who the identifier belongs to—her actual identity is still protected by the anonymity service—but they can still observe page views and patterns because multiple payments on a payment channel are inherently linkable. This might be enough to uniquely identify Alice (e.g. if she looks at documents related to newspaper articles she wrote), or it could reveal other information—like what subject she is writing an article on. Thus Zcash is <em>part</em> of the solution, but Zcash itself does not a private payment channel make.</p>
</div>
<div class="section" id="bolt-private-payment-channels">
<h2>BOLT: Private Payment Channels</h2>
<p>Enter BOLT, which Matt and I have been working on for the past few months. BOLT eliminates the linkage between payments within a channel. This ensures that Alice’s payments are hidden within the set of <em>all</em> payments made to that recipient.</p>
<p>We have designed two protocols, one that is non-interactive but only allows payment from Alice to Bob of fixed values, and one that allows bidirectional payments of arbitrary values but requires interaction. We will focus on the bidirectional protocol here.</p>
<p>The basic idea of the protocol is to build private IOUs. We do this using two pieces of technology: blind signatures and commitments. Commitments allow Alice to hide the value of the IOU (which could identify it). Blind signatures convince Bob the IOU is authentic —because he must have signed it—but ensure that he cannot recognize the signature or IOU specifically out of any of the set of IOUs he signed.</p>
<div class="figure align-right">
<img alt="BOLT Diagram" src="/wp-content/uploads/2016/08/bolt2.png"/></div>
<p>Alice pays Bob by proving she has such an IOU, invalidating it (by signing it with the Revocation key), and getting Bob to sign a new IOU with a balance that is the same as the old one less the amount of payment. Similarly, when Bob pays Alice the amount is added to the new IOU. The actual balance and signature remains hidden from Bob, ensuring he cannot tell if two distinct payments came from the same channel or different ones.</p>
<p>The real challenge is invalidating the old IOU and signing the new one atomically. And—this is the hard part—doing it without leaking which channel Alice is using. If Alice invalidates the old IOU first, and Bob refuses to sign the new IOU, Alice cannot close the channel so she loses her money. If Bob signs the new IOU before the old one is invalidated, then Alice can defraud Bob:  She can then take the new IOU Bob signed and use it for a series of payments, but then cash out the original IOU keeping all her money. In normal payment channels, this cannot happen because Bob will recognize Alice’s subsequent fraudulent payments. Doing so for private channels, however, is impossible.</p>
<p><img alt="BOLT Diagram" src="/wp-content/uploads/2016/08/bolt.png"/></p>
<p>To solve this, we separate the process of generating IOUs for channel closure from allowing the IOUs to be used for future transactions. An IOU is a commitment to both the balance and a one-time-use public key called the revocation key. We assume Alice has an existing (blindly) signed IOU from channel establishment.  ① Alice first creates a new IOU and proves that it pays Bob $5 more than some IOU Bob signed previously. ② Alice then provably reveals the revocation public key of the old IOU and gets ③ Bob to sign the new IOU for closure (after of course proving the new IOU is correctly formed with respect to the old one). ④ Then she signs a message invalidating the old IOU with the revocation key and gives the message + signature to Bob. This is safe because she can now close the channel with the new IOU no matter what happens. ⑤ After ensuring the old IOU is revoked, Bob now signs the new IOU as valid for use in the next payment. This is safe because the old IOU is invalid and thus Bob is assured Alice can never revert back to an old state where she has more money. Alice can now use the new IOU in the next BOLT payment.</p>
<p>From Bob's perspective, he knows that he has received a payment (of $5 in this example) on one of his payment channels (or rather, he <em>will</em> receive $5 more when that payment channel is closed) but he doesn't know which payment channel was actually used for the payment : we’ve hidden the actual IOU, its balance, and Bob’s signature on it from him and these are the only ways he could identify the channel.</p>
<p>The interesting part is all of this is simple, fast, and uses very well understood crypto. A prototype will be released soon, but we believe it will take less than 50 ms and 10 MB of memory to execute this protocol.</p>
</div>
<div class="section" id="indirect-payment-channels">
<h2>Indirect Payment Channels</h2>
<p>So far, we require Alice and Bob to have a payment channel. But what if they don’t?</p>
<p>Like Lightning, BOLT allows payments when there is no direct channel between parties, provided they share an intermediary (e.g. Coinbase). We do this by making the IOUs’ usage for channel closure conditional on the other transactions going through. Unlike Lightning, a single intermediary learns neither the participants involved nor the amount transferred. To do this, it’s crucial that the channels themselves are funded anonymously, as the third party can abort and observe who closes their channel. If the channel itself is anonymous, this information is worthless.</p>
<p>It is likely we can generalize BOLT’s indirect payments to payments via multiple intermediaries, as in Lightning, but at the moment BOLT does not do so.</p>
</div>
<div class="section" id="can-bolt-work-without-zcash">
<h2>Can BOLT work without Zcash?</h2>
<p>We can set up BOLT to work with most cryptocurrencies provided we can add the primitives. We might even be able to do this without any changes to Bitcoin, though at the cost of using hash-based commitments and generic circuit-based multi-party computation (MPC) for blind signing with ECDSA. But any real privacy provided by BOLT fundamentally depends on channel establishment and closure being anonymous.</p>
<p>In Bitcoin, funding a channel is not private: there is a record of who you opened the channel with, the amount, and what it closed for. BOLT alone does not solve this problem—it only makes payments on the same channel unlinkable to each other.  Worse, if a merchant or third party can force an abort in the BOLT protocol, then they can identify which channel you are using. They can only do this once, so multiple payments on the same channel cannot be linked, but if you did not open the channel anonymously, then that (aborted) payment can be linked to you.</p>
<p>To avoid this, you need anonymous funds to create the channel. Indeed, the privacy requirements for funding a channel are as high as those for normal payments. So you want as strong privacy as you would for normal payments. And Zcash is the best way to get strongly private funds.</p>
<p>I’d like to thank Sean Bowe, one of the Zcash developers, for suggesting the idea of combining Lightning and Zerocash. And Sean, Maureen, Matthew, Daira, Jack, and the anonymous leopard for feedback on this blog post.</p>
</div>
