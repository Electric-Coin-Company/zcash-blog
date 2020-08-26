---
ID: 4893
post_title: BIP199 for Hashed Timelocked Contracts
post_name: htlc-bip
post_date: 2017-03-29 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/htlc-bip/
published: true
tags:
  - bitcoin
  - XCAT
categories:
  - General
---
<p>Hashed Timelocked Contracts (HTLC) are a well-known and simple technique for building protocols for atomic swaps. They allow you to pay another party for some information (generally, a key) with a condition that allows you to receive your money back if the party does not cooperate.</p>
<p>HTLCs are a fundamental tool in the Lightning network, in zero-knowledge contingent payments (ZKCP) like the one we performed <a class="reference external" href="/blog/science-roundup">last year</a> at FC'16, and in our XCAT project <a class="reference external" href="/blog/the-near-future-of-zcash">that we announced last month</a>. One of the first steps forward is the inclusion of general HTLC functionality in the Bitcoin Core wallet.</p>
<p>This week, our submitted BIP199 draft was merged. We also have a work-in-progress <a class="reference external" href="https://github.com/bitcoin/bitcoin/pull/7601">reference implementation</a> in the Bitcoin Core wallet. HTLCs can be used today without any changes to the Bitcoin protocol, so these proposals and implementations are for standardizing best practices and ecosystem compatibility.</p>
<p>Check out the current BIP text here: <a class="reference external" href="https://github.com/bitcoin/bips/blob/master/bip-0199.mediawiki">https://github.com/bitcoin/bips/blob/master/bip-0199.mediawiki</a></p>
<div class="section" id="overview-of-htlc">
<h2>Overview of HTLC</h2>
<p>HTLC scripts look like this:</p>
<table class="codehilitetable">
<tr>
<td class="linenos">
<div class="linenodiv">
<pre>1
2
3
4
5
6
7</pre>
</div>
</td>
<td class="code">
<div class="codehilite">
<pre><span/>OP_IF
    [HASHOP] &lt;digest&gt; OP_EQUALVERIFY OP_DUP OP_HASH160 &lt;seller pubkey hash&gt;
OP_ELSE
    &lt;num&gt; [TIMEOUTOP] OP_DROP OP_DUP OP_HASH160 &lt;buyer pubkey hash&gt;
OP_ENDIF
OP_EQUALVERIFY
OP_CHECKSIG
</pre>
</div>
</td>
</tr>
</table>
<p>HASHOP is a hashing algorithm (RIPEMD, SHA256), and TIMEOUTOP is either OP_CHECKLOCKTIMEVERIFY or OP_CHECKSEQUENCEVERIFY. This script allows the "buyer" to purchase the preimage to &lt;digest&gt; by forcing the seller to reveal it when they claim their funds. If the seller doesn't reveal it, the buyer can get their money back after the timeout period.</p>
<p>It's easy to see how cross-chain atomic swaps can be built with this mechanism:</p>
<ol class="arabic simple">
<li>Alice randomly samples K, the key. She hashes it, producing X.</li>
<li>Alice creates a transaction paying Bob 1 BTC, with a timeout of 1 day, to produce the preimage of X.</li>
<li>Bob waits for Alice's transaction to appear in the Bitcoin blockchain, and then submits an HTLC transaction paying Alice 0.02 ZEC for the preimage of X with a smaller timeout of half a day.</li>
<li>Once Bob's transaction appears in the Zcash blockchain, Alice can obtain her ZEC. The script forces her to reveal K.</li>
<li>Once Bob sees Alice's reveal of K, he can obtain his BTC.</li>
</ol>
<p>The timeouts are selected so that Bob always has an opportunity to obtain a refund before Alice. Otherwise, Alice could wait to obtain her refund, and then claim Bob's money by revealing K.</p>
<p>Having contracts like HTLCs standardized and included in Bitcoin and Zcash will help both of our communities build exciting technologies like decentralized exchanges.</p>
</div>
