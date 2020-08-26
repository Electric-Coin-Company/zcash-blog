---
ID: 4907
post_title: 'New Beta Release: Fixes, Packaging and Launch Preparation'
post_name: >
  new-beta-release-fixes-packaging-and-launch-preparation
post_date: 2016-10-17 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-beta-release-fixes-packaging-and-launch-preparation/
published: true
tags:
  - beta
  - deterministic builds
  - releases
  - Tor
categories:
  - General
---
<p>Today, we deployed the third beta release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <cite>1.0.0-rc1</cite>, to the testnet. This is the third release of the Zcash Beta Series. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple">
<li>We added a script to create a Zcash Debian package. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1448">#1448</a>)</li>
<li>We have published the first release of our <a class="reference external" href="/blog/deterministic-builds/">Gitian-based deterministic build environment</a> and updated libsnark to support it. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1521">#1521</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1543">#1543</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1541">#1541</a>)</li>
<li>We have renamed the client identifier from “Satoshi” to “Magic Bean”. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1481">#1481</a>)</li>
<li>We have made the 100kb transaction size limit a consensus rule, rather than a standard rule. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1501">#1501</a>)</li>
<li>Fixed UTXO selection and improved error reporting surrounding the consensus rule that coinbase UTXOs must be sent to a zaddr. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1431">#1431</a>)</li>
<li>Added JoinSplits to the JSON output of the RPC call gettransaction. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1493">#1493</a>)</li>
<li>The ‘account’ parameter in RPC calls is now deprecated. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1490">#1490</a>)</li>
<li>Debug log messages for z_* RPC calls can be viewed with option -debug=”zrpc”. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1523">#1523</a>)</li>
<li>Fixed a bug in encrypted wallets by caching nullifiers.  (<a class="reference external" href="https://github.com/zcash/zcash/pull/1520">#1520</a>)</li>
<li>Added fixes to address a bug with note witnesses in the wallet. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1526">#1526</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1547">#1547</a>)</li>
<li>Fixed an issue where some tests where outputting data to local directory.  (<a class="reference external" href="https://github.com/zcash/zcash/pull/1506">#1506</a>)</li>
<li>We have updated documentation related to Tor,  the release process, security risks and wallet reindexing. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1483">#1483</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1511">#1511</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1499">#1499</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1492">#1492</a>)</li>
</ol>
<p>Note that this release does not reset the beta testnet and continues to uses the beta 2 proving and verify keys. <strong>NOTE:</strong> <cite>It does however make a change to the local block index format that will cause all upgraded nodes to fail to start (because they can’t parse the old block index format). As the error message will say, please start up your node once with the reindex flag after upgrading (ie.</cite> <tt class="docutils literal">./src/zcashd <span class="pre">-reindex</span></tt> <cite>) to resolve this issue.</cite></p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestone/39">1.0.0-rc1</a> release github milestone.</td>
</tr>
</tbody>
</table>
