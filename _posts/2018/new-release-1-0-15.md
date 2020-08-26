---
ID: 4997
post_title: 'New Release: 1.0.15'
post_name: new-release-1-0-15
post_date: 2018-03-02 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-1-0-15/
published: true
tags:
  - Overwinter
  - releases
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.15, which contains the Overwinter consensus rules with a testnet activation height. It also includes various bug fixes, and adds an experimental RPC method for merging UTXOs and notes.</p>
<h2>Notable changes</h2>
<h3>Overwinter network upgrade</h3>
<p>The code preparations for the Overwinter network upgrade, as described in <a href="https://github.com/zcash/zips/blob/master/zip-0200.rst">ZIP 200</a>, <a href="https://github.com/zcash/zips/blob/master/zip-0201.rst">ZIP 201</a>, <a href="https://github.com/zcash/zips/blob/master/zip-0202.rst">ZIP 202</a>, <a href="https://github.com/zcash/zips/blob/master/zip-0203.rst">ZIP 203</a>, and <a href="https://github.com/zcash/zips/blob/master/zip-0143.rst">ZIP 143</a> are finished and included in this release. Overwinter will activate on testnet at height 207500, and can also be activated at a specific height in regtest mode by setting the config option <code>-nuparams=5ba81b19:HEIGHT</code>.</p>
<p>However, because the Overwinter activation height is not yet specified for mainnet, version 1.0.15 will behave similarly as other pre-Overwinter releases even after a future activation of Overwinter on the network. Upgrading from 1.0.15 will be required in order to follow the Overwinter network upgrade on mainnet.</p>
<h3>Overwinter transaction format</h3>
<p>Once Overwinter has activated, transactions must use the new v3 format (including coinbase transactions). All RPC methods that create new transactions (such as <code>createrawtransaction</code> and <code>getblocktemplate</code>) will create v3 transactions once the Overwinter activation height has been reached.</p>
<h3>Overwinter transaction expiry</h3>
<p>Overwinter transactions created by <code>zcashd</code> will also have a default expiry height set (the block height after which the transaction becomes invalid) of 20 blocks after the height of the next block. This can be configured with the config option <code>-txexpirydelta</code>.</p>
<h3>UTXO and note merging</h3>
<p>In order to simplify the process of combining many small UTXOs and notes into a few larger ones, a new RPC method <code>z_mergetoaddress</code> has been added as an experimental feature. It merges funds from t-addresses, z-addresses, or both, and sends them to a single t-address or z-address. To test it out, set the config option <code>-zmergetoaddress</code> (as well as enabling experimental features). We encourage mining pools and exchanges to test it out over the next few weeks, and give feedback, before we make it a fully-supported RPC method in an upcoming release.</p>
<p>Unlike most other RPC methods, <code>z_mergetoaddress</code> operates over a particular quantity of UTXOs and notes, instead of a particular amount of ZEC. By default, it will merge 50 UTXOs and 10 notes at a time; these limits can be adjusted with the parameters <code>transparent_limit</code> and <code>shielded_limit</code>.</p>
<p><code>z_mergetoaddress</code> also returns the number of UTXOs and notes remaining in the given addresses, which can be used to automate the merging process (for example, merging until the number of UTXOs falls below some value).</p>
<h3>UTXO memory accounting</h3>
<p>The default <code>-dbcache</code> has been changed in this release to 450MiB. Users can set <code>-dbcache</code> to a higher value (e.g. to keep the UTXO set more fully cached in memory). Users on low-memory systems (such as systems with 1GB or less) should consider specifying a lower value for this parameter.</p>
<p>Additional information relating to running on low-memory systems can be found here: <a href="https://github.com/zcash/zcash/blob/master/doc/reducing-memory-usage.md">reducing-memory-usage.md</a>.</p>
<h3>Summary of the changes included in this release</h3>
<ol>
<li>We implemented the Overwinter network upgrade consensus rules and transaction version. (<a href="https://github.com/zcash/zcash/pull/2874">#2874</a>, <a href="https://github.com/zcash/zcash/pull/2898">#2898</a>, <a href="https://github.com/zcash/zcash/pull/2903">#2903</a>, <a href="https://github.com/zcash/zcash/pull/2925">#2925</a>, <a href="https://github.com/zcash/zcash/pull/3002">#3002</a>)</li>
<li>We added logic to the mempool to evict transactions that can't be mined into the current branch. (<a href="https://github.com/zcash/zcash/pull/2940">#2940</a>)</li>
<li>We added logic to preferentially evict pre-Overwinter nodes shortly before activation, and disconnect from them after activation. (<a href="https://github.com/zcash/zcash/pull/2919">#2919</a>)</li>
<li>We added information about network upgrades and version deprecation to the RPC interface. (<a href="https://github.com/zcash/zcash/pull/2808">#2808</a>, <a href="https://github.com/zcash/zcash/pull/2839">#2839</a>)</li>
<li>We fixed a bug where a block index field was not being read from disk. (<a href="https://github.com/zcash/zcash/pull/2931">#2931</a>, <a href="https://github.com/zcash/zcash/pull/2977">#2977</a>, <a href="https://github.com/zcash/zcash/pull/2993">#2993</a>)</li>
<li>We implemented a roll-back limit for reorganization and branch rewinding of 100 blocks. (<a href="https://github.com/zcash/zcash/pull/2463">#2463</a>)</li>
<li>We added <code>z_mergetoaddress</code> as an experimental feature. (<a href="https://github.com/zcash/zcash/pull/2797">#2797</a>)</li>
<li>We increased the default value of <code>-dbcache</code>. (<a href="https://github.com/zcash/zcash/pull/2873">#2873</a>)</li>
</ol>
