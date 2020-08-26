---
ID: 5027
post_title: 'New Release: 2.0.0'
post_name: new-release-2-0-0
post_date: 2018-08-16 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-0/
published: true
tags:
  - bugs
  - Overwinter
  - releases
  - Sapling
categories:
  - Technical
---
<p>We're happy to announce the release of Zcash 2.0.0, the first Sapling-compatible version of the Zcash node software!</p>
<h2>Sapling Activation</h2>
<h3>Mainnet</h3>
<p>This release is consensus-compatible with the Sapling network upgrade, and so we're encouraging all users and miners to upgrade as soon as possible. The first block of Sapling will be block 419200, which is expected to be mined on the 28th of October 2018, the second anniversary of Zcash's official launch. You can read more about the Sapling network upgrade <a href="/blog/whats-new-in-sapling/">here</a> or on the <a href="https://z.cash/upgrade/sapling.html">Sapling Network Upgrade</a> page.</p>
<h3>Testnet</h3>
<p>Sapling will activate on the testnet at block 280000, which is expected about a week after this release. Sapling had previously activated on testnet, but because changes were made to the consensus rules your node will automatically roll back and proceed on the Overwinter testnet branch until Sapling activates again at the new height.</p>
<h2>Other Notable Changes</h2>
<h3>Experimental Sapling RPC Support</h3>
<p>This release contains only experimental support for Sapling RPC functionality. Full support for Sapling RPC functionality will appear in the 2.0.1 release.</p>
<p>Developers must specify <code>-experimentalfeatures</code> and <code>-developersapling</code> to use the existing functionality on testnet after activation. Alternatively, developers can use these features in regtest mode.</p>
<h3>Fix Peer Banning Bug Introduced In Overwinter</h3>
<p>After Overwinter activation, nodes syncing from a block height prior to the activation height (347500) experienced slow syncing due to a peer banning mechanism that was introduced to mitigate against a class of DoS attacks from Sprout nodes. This fix replaces the use of peer banning with behavior to ignore invalid transactions.</p>
<h2>Summary of the Changes Included in this Release</h2>
<ol>
<li>Set the Sapling activation height for mainnet and testnet. (<a href="https://github.com/zcash/zcash/pull/3469">#3469</a>)</li>
<li>Adopted the official Sapling system parameters. (<a href="https://github.com/zcash/zcash/pull/3448">#3448</a>)</li>
<li>Added support for rollbacks of testnet. (<a href="https://github.com/zcash/zcash/pull/3443">#3443</a>)</li>
<li>Added experimental wallet support for Sapling z-addresses. (<a href="https://github.com/zcash/zcash/pull/3273">#3273</a>, <a href="https://github.com/zcash/zcash/pull/3353">#3353</a>, <a href="https://github.com/zcash/zcash/pull/3392">#3392</a>, <a href="https://github.com/zcash/zcash/pull/3429">#3429</a>, <a href="https://github.com/zcash/zcash/pull/3396">#3396</a>, <a href="https://github.com/zcash/zcash/pull/3458">#3458</a>)</li>
<li>Added experimental support for building Sapling transactions. (<a href="https://github.com/zcash/zcash/pull/3417">#3417</a>)</li>
<li>Added experimental support for Sapling note encryption and decryption. (<a href="https://github.com/zcash/zcash/pull/3324">#3324</a>, <a href="https://github.com/zcash/zcash/pull/3391">#3391</a>)</li>
<li>Accept the transaction expiry height as a parameter to RPC call <code>createrawtransaction</code>. (<a href="https://github.com/zcash/zcash/pull/3336">#3336</a>)</li>
<li>Prepared the codebase for <a href="https://github.com/zcash/zips/pull/157">ZIP 32</a> integration, including bumping the Rust compiler version to 1.28. (<a href="https://github.com/zcash/zcash/pull/3447">#3447</a>)</li>
<li>Begin checking the zk-SNARK parameter hash when loaded into memory. (<a href="https://github.com/zcash/zcash/pull/3441">#3441</a>)</li>
<li>Always record the best Sapling anchor on disk even if it is for the empty tree, because rollbacks may occur. (<a href="https://github.com/zcash/zcash/pull/3463">#3463</a>)</li>
<li>Fixed a bug where nodes may ban peers during synchronization before network upgrade activation. (<a href="https://github.com/zcash/zcash/pull/3410">#3410</a>)</li>
<li>Backport upstream improvements to <code>InitialBlockDownload</code>. (<a href="https://github.com/zcash/zcash/pull/3263">#3263</a>)</li>
<li>Update the mainnet checkpoints to improve the speed of initial synchronization. (<a href="https://github.com/zcash/zcash/pull/3246">#3246</a>)</li>
</ol>
<p>We're encouraging all users and miners to upgrade to this new version.  See the <a href="https://z.cash/download.html">download</a> page for more information.</p>
<p>For a more complete list of changes, see the <a href="https://github.com/zcash/zcash/milestone/73?closed=1">2.0.0</a> GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
<p>&nbsp;</p>
