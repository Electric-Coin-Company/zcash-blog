---
ID: 5013
post_title: 'New Release: 1.1.1'
post_name: new-release-1-1-1
post_date: 2018-05-30 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-1-1-1/
published: true
tags:
  - bugs
  - Overwinter
  - releases
  - Sapling
categories:
  - General
---
<p>Zcash 1.1.1 has arrived!  This release is an Overwinter-compatible version of the Zcash node software, with initial support for Sapling consensus rules and a Sapling testnet activation height set to block 252500.</p>
<h2>Overwinter network upgrade</h2>
<p>The first block of Overwinter will be block 347500, which is expected to be mined on the 25th of June 2018. Please upgrade to this release, or any release from v1.1.0 onwards, in order to follow the Overwinter network upgrade. See our <a href="/blog/overwinter/" rel="nofollow">previous blog post</a> and the <a href="https://z.cash/upgrade/overwinter.html" rel="nofollow">Overwinter Network Upgrade page</a> for more information.</p>
<h2>Developers preparing for Sapling</h2>
<h3>Sapling network upgrade</h3>
<p>The consensus code preparations for the Sapling network upgrade, as described in <a href="https://github.com/zcash/zips/blob/master/zip-0243.rst">ZIP 243</a> and the <a href="https://github.com/zcash/zips/blob/master/protocol/sapling.pdf">Sapling spec</a> are finished and included in this release. Sapling support in the wallet and RPC is ongoing, and is expected to land in master over the next few weeks.</p>
<p>The <a href="/blog/announcing-the-sapling-mpc/" rel="nofollow">Sapling MPC</a> is currently working on producing the final Sapling parameters. In the meantime, Sapling will activate on testnet with dummy Sapling parameters at height 252500. This activation will be temporary, and the testnet will be rolled back by version 2.0.0 so that both mainnet and testnet will be using the same parameters. Users who want to continue testing Overwinter should continue to run version 1.1.0 on testnet, and then upgrade to 2.0.0 (which will be released after Overwinter activates).</p>
<p style="text-align: left;">Sapling can also be activated at a specific height in regtest mode by setting the config options <code>-nuparams=5ba81b19:HEIGHT -nuparams=76b809bb:HEIGHT</code>. These config options will change when the testnet is rolled back for 2.0.0 (because the branch ID for Sapling will change, due to us following the safe upgrade conventions we introduced in Overwinter).</p>
<p style="text-align: left;">Users running testnet or regtest nodes will need to run <code>./zcutil/fetch-params.sh --testnet</code> (for users building from source) or <code>zcash-fetch-params --testnet</code> (for binary / Debian users).</p>
<p style="text-align: left;">As a reminder, because the Sapling activation height is not yet specified for mainnet, version 1.1.1 will behave similarly as other pre-Sapling releases even after a future activation of Sapling on the network. Upgrading from 1.1.1 will be required in order to follow the Sapling network upgrade on mainnet.</p>
<h3>Sapling transaction format</h3>
<p>Once Sapling has activated, transactions must use the new v4 format (including coinbase transactions).  All RPC methods that create new transactions (such as <code>createrawtransaction</code> and <code>getblocktemplate</code>) will create v4 transactions once the Sapling activation height has been reached.</p>
<h2>Other notable changes</h2>
<h3>zcash-cli: arguments privacy</h3>
<p>The RPC command line client gained a new argument, <code>-stdin</code> to read extra arguments from standard input, one per line until EOF/Ctrl-D.  For example:</p>
<pre><code>$ src/zcash-cli -stdin z_importkey
mysecretzkey
yes
200000
^D (Ctrl-D)
</code></pre>
<p>It is recommended to use this for sensitive information such as private keys, as command-line arguments can usually be read from the process table by any user on the system.</p>
<h3>Asm representations of scriptSig signatures now contain SIGHASH type decodes</h3>
<p>The <code>asm</code> property of each scriptSig now contains the decoded signature hash<br />
type for each signature that provides a valid defined hash type.</p>
<p>The following items contain assembly representations of scriptSig signatures<br />
and are affected by this change:</p>
<ul>
<li>RPC <code>getrawtransaction</code></li>
<li>RPC <code>decoderawtransaction</code></li>
<li>REST <code>/rest/tx/</code> (JSON format)</li>
<li>REST <code>/rest/block/</code> (JSON format when including extended tx details)</li>
<li><code>zcash-tx -json</code></li>
</ul>
<p>For example, the <code>scriptSig.asm</code> property of a transaction input that<br />
previously showed an assembly representation of:</p>
<pre><code>304502207fa7a6d1e0ee81132a269ad84e68d695483745cde8b541e3bf630749894e342a022100c1f7ab20e13e22fb95281a870f3dcf38d782e53023ee313d741ad0cfbc0c509001
</code></pre>
<p>now shows as:</p>
<pre><code>304502207fa7a6d1e0ee81132a269ad84e68d695483745cde8b541e3bf630749894e342a022100c1f7ab20e13e22fb95281a870f3dcf38d782e53023ee313d741ad0cfbc0c5090[ALL]
</code></pre>
<p>Note that the output of the RPC <code>decodescript</code> did not change because it is<br />
configured specifically to process scriptPubKey and not scriptSig scripts.</p>
<h2>Summary of the changes included in this release</h2>
<ol>
<li>We set the Sapling testnet activation height to block 252500. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3305">#3305</a>)</li>
<li>We removed the 100kB transaction size limit from Sapling activation. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3212">#3212</a>)</li>
<li>We implemented Sapling consensus rules. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/issues/3207">#3207</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3220">#3220</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3232">#3232</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3255">#3255</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3275">#3275</a>)</li>
<li>We implemented Sapling merkle tree, nullifiers and added support for v4 transactions and loading Sapling parameters. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3170">#3170</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3191">#3191</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3197">#3197</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3169">#3169</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3185">#3185</a>)</li>
<li>We implemented ZIP 243 for Sapling signature hashing. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3233">#3233</a>)</li>
<li>We updated support for Sprout shielded transactions to use the Groth16 proving system when Sapling activates. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3251">#3251</a>)</li>
<li>We backported transparent address refactors, and are in the process of adding support for Sapling keys, addresses and notes. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3206">#3206</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3234">#3234</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/issues/3123">#3123</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3228">#3228</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3202">#3202</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3242">#3242</a>)</li>
<li>We extended a mempool eviction RPC test to cover Sapling activation. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3074">#3074</a>)</li>
<li>We backported improvements to RPC call <code>getblock</code>. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3179">#3179</a>)</li>
<li>We updated the Payment API documentation. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3264">#3264</a>)</li>
<li>We resolved Least Authority auditor issues C, D and E. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3160">#3160</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3181">#3181</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3183">#3183</a>)</li>
<li>We updated the build process to use Rust 1.26 stable. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3271">#3271</a>)</li>
<li>We fixed bugs on several unsupported platforms. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/2784">#2784</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3153">#3153</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3227">#3227</a>)</li>
<li>We extended Sprout tests to other epochs. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3157">#3157</a>)</li>
<li>We backported improvements to <code>zcash-cli</code>, serialization, out-of-memory error reporting and the configuration option <code>uacomment</code>. (<a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3086">#3086</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3180">#3180</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/3193">#3193</a>, <a class="issue-link js-issue-link" href="https://github.com/zcash/zcash/pull/2813">#2813</a>)</li>
</ol>
<p>We’re encouraging all users and miners to update to this version. See the <a class="reference external" href="https://z.cash/download.html">download</a> page and <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see the <a href="https://github.com/zcash/zcash/milestone/71?closed=1">1.1.1</a> GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
