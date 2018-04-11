---
ID: 1616
post_title: Science Roundup
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/science-roundup/
published: true
post_date: 2016-03-18 00:00:00
---
<p>We are a science-driven company, and our team is always working on advancing the forefront of human knowledge. Here is a round-up of science news from our team.</p>
<div class="section" id="zero-knowledge-contingent-payments">
<h2>Zero-Knowledge Contingent Payments</h2>
<img alt="ZKCP Demo at FC16 Bitcoin Workshop" src="http://blog.z.cash/wp-content/uploads/2016/03/zkcp-demo.png"/><p>Zcasher <em>Sean Bowe</em>, working with Greg Maxwell and Peter Wuille (both of Blockstream and Bitcoin Core) demoed the first zero-knowledge contingent payment on the Bitcoin network. Also referred to as ZKCP, this payment protocol (invented by Greg Maxwell) is a reliable way for two parties to exchange information and money <em>atomically</em>.</p>
<p>In the demo performed live at Financial Cryptography 2016, Sean and Greg (remotely) swapped the solution to a 16x16 sudoku puzzle for 0.1 Bitcoin.</p>
<p>Such an atomic swap of money for information <em>without either party being vulnerable to someone else</em> has never before been possible. Before ZKCP, the only way that money and information could be swapped was for one side to hand over their goods first, thus risking that the other side would cheat and keep both, or for both sides to agree on a third party escrow agent that they would each hand over their goods to, and rely on that third party to act honestly.</p>
<p>In addition to being atomic, ZKCP is also private. In ZKCP, only the buyer and the seller learn the content of the information being swapped. This makes it private in a way that is currently not possible with a smart-contracting system like Ethereum.</p>
<p>I'm excited about this demo because it shows that zero-knowledge proofs are a flexible and powerful tool that may find many different kinds of applications beyond Zcash. In this implementation, Sean used the same kinds of tools for constructing zero-knowledge proofs that we use for Zcash, such as <a class="reference external" href="https://github.com/scipr-lab/libsnark">libsnark</a>.</p>
<p>Sean also submitted a <a class="reference external" href="https://github.com/bitcoin/bitcoin/pull/7601">pull-request to Bitcoin Core</a> which provides support for HTLC (Hashed Timelock Contracts) used by ZKCP and other protocols like Paypub and Lightning.</p>
<p>For more details, please read <a class="reference external" href="https://bitcoincore.org/en/2016/02/26/zero-knowledge-contingent-payments-announcement/">Greg's blog post</a> on the Bitcoin Core blog.</p>
</div>
<div class="section" id="remote-key-extraction-via-side-channel-attacks">
<h2>Remote Key Extraction via Side Channel Attacks</h2>
<div class="align-left figure" style="width: 25%">
<img alt="don't let this guy stand next to your laptop or phone" src="http://blog.z.cash/wp-content/uploads/2016/03/eran.jpg"/></div>
<p>Zcasher <em>Eran Tromer</em> and co-authors have published two new papers about side-channel attacks, one attacking GPG and another attacking ECDSA. Using small and non-intrusive sensors, the electromagnetic emanations of the device are analyzed and private keys are derived from the signals.</p>
<p>The attacks were detailed in two papers, <a class="reference external" href="https://www.tau.ac.il/~tromer/mobilesc/">"ECDSA Key Extraction from Mobile Devices via Nonintrusive Physical Side Channels"</a> and <a class="reference external" href="https://www.tau.ac.il/~tromer/ecdh/">"ECDH Key-Extraction via Low-Bandwidth Electromagnetic Attacks on PCs"</a>.</p>
<div class="align-right figure" style="width: 45%">
<img alt="Phone Key Stealer" src="http://blog.z.cash/wp-content/uploads/2016/03/cheap-iphone4-glass-top-w600.jpg"/></div>
<p>The ECDSA attack was able to steal the secret key out of a Bitcoin wallet that was running on a phone sitting on a glass tabletop. We notified the Bitcoin Core team about this attack and confirmed that Bitcoin Core since v0.10.0 is safe from this attack.</p>
<p>These are powerful, practical attacks that underscore that danger lies ahead for software vulnerable to side-channel attacks.</p>
</div>
<div class="section" id="honey-badger-bft">
<h2>Honey Badger BFT</h2>
<div class="align-left figure" style="width: 25%">
<img alt="the friendly author for the latest and greatest BFT" src="http://blog.z.cash/wp-content/uploads/2016/03/amiller.png"/></div>
<p>Zcasher <em>Andrew Miller</em> and his co-authors released a pre-print paper draft of <a class="reference external" href="https://eprint.iacr.org/2016/199">"The Honey Badger of Byzantine Fault Tolerance Protocols"</a>. They've invented a Byzantine Fault Tolerance protocol that does not have hard-coded timeouts. This means that the system can operate normally, and retain its fault-tolerance properties, even when the network has worse latency than anticipated.</p>
<p>It also means that in case of a temporary network interruption, Honey Badger BFT recovers quickly compared to other Byzantine Fault Tolerance protocols.</p>
<div class="align-right figure" style="width: 25%">
<img alt="the friendly mascot for the latest and greatest BFT" src="http://blog.z.cash/wp-content/uploads/2016/03/honeybadgerbft.png"/></div>
<p>Honey Badger BFT may eventually be applicable to cryptocurrencies — where in future designs it could potentially serve as a high-performance BFT protocol in a hybrid mode with a more expensive censorship-resistant protocol. It may also be applicable to “blockchain” use cases, where a group of participants need a robust and efficient agreement protocol, but don't need censorship-resistance.</p>
</div>
<div class="section" id="conclusion">
<h2>Conclusion</h2>
<p>That's just the most recent batch of science results from Zcashers. Stay tuned for the next batch!</p>
<p>— Zooko Wilcox, March 18, 2016</p>
</div>