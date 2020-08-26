---
ID: 4867
post_title: An Update on Atomic Trades
post_name: atomic-trades
post_date: 2017-09-11 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/atomic-trades/
published: true
tags:
  - tools
  - XCAT
categories:
  - General
---
<p>Decentralization is a key characteristic of cryptocurrencies because it removes dependence on trusting third parties in order to transact between individuals. However, exchanges between different cryptocurrencies typically still require trust in a centralized exchange or counterparty. Cross-chain <a class="reference external" href="https://en.bitcoin.it/wiki/Atomic_cross-chain_trading">atomic trades</a> (for which we have coined the acronym “XCATs”) remove the need for a single point of trust for trades between different cryptocurrencies. They rely on clever protocols that automatically exchange funds across two chains only if both participants hold up their end of the deal, and refund both participants otherwise. To support the decentralization of cryptocurrency, one of our <a class="reference external" href="/blog/the-near-future-of-zcash/">near-term goals</a> is to develop tools that will help carry out atomic trades across blockchains. <a class="footnote-reference" href="#id2" id="id1">[1]</a></p>
<div class="section" id="zcash-bitcoin-atomic-trades">
<h2>Zcash &lt;-&gt; Bitcoin Atomic Trades</h2>
<p>We are excited to announce that we have been working on a command-line tool that executes atomic trades between Zcash t-addrs and Bitcoin addresses (view our recent <a class="reference external" href="https://www.youtube.com/watch?v=nPvfn138PRg">demo</a> of the tool). Several people have come up with XCAT protocols. Loosely speaking, they all rely on a mechanism where for one side to obtain their coins, a secret must be revealed that will enable the second party to also redeem their coins. There are many variants of this basic idea; see our <a class="reference external" href="https://github.com/arcalinea/zips/blob/b1ac22dab7ac00a9d07d05c63c3b1f5a0d619967/drafts/arcalinea-xcat/draft.rst">XCAT ZIP</a> for a detailed description of the specific protocol we use. Meanwhile, you are encouraged to try the experimental version of our tool, <a class="reference external" href="https://github.com/zcash/zbxcat">ZBXCAT</a>, and report problems or ask questions on the <a class="reference external" href="https://chat.zcashcommunity.com/channel/alchemy">alchemy channel</a> of our community chat. The current version requires the user to run Bitcoin and Zcash full nodes, but a light-client version is in progress.</p>
<p>The way that funds are locked up on the blockchain to do atomic trades relies on <a class="reference external" href="/blog/htlc-bip/">hash-time lock contracts (HTLC)</a>. Zcash engineer Sean Bowe has submitted a BIP and pull request to make HTLCs a part of the standard RPC interface in the Bitcoin core client. However, it is not necessary to wait for this PR to be merged, as raw HTLC transactions can be constructed by compiling non-standard pay-to-script-hash transactions. We used python-bitcoinlib and a variant of it modified for Zcash to construct these scripts: <a class="reference external" href="https://github.com/arcalinea/python-zcashlib">https://github.com/arcalinea/python-zcashlib</a></p>
<p>To see an example of the redeem scripts used, view the scriptsig of this bitcoin transaction. This was one of the four transactions in the first atomic trade performed on testnet using our script, with the participation of community volunteer Jason Davies:</p>
<p><a class="reference external" href="https://www.blocktrail.com/tBTC/tx/a0a2079411d73ec056e6a4ca0c9f9046056e652eb173c28165fb665c81af98f2">https://www.blocktrail.com/tBTC/tx/a0a2079411d73ec056e6a4ca0c9f9046056e652eb173c28165fb665c81af98f2</a></p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>We note that other groups have done/are doing excellent work on cross-chain trades, for example, <a class="reference external" href="https://www.supernet.org/en/technology/whitepapers/barterdex-a-practical-native-dex#atomic-cross-chain-protocol">barterDEX</a>.</td>
</tr>
</tbody>
</table>
</div>
