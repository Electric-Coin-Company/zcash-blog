---
ID: 1602
post_title: 'New Release Candidate: Less than One Week to Launch'
author: Daira Hopwood
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-release-candidate-less-than-one-week/
published: true
post_date: 2016-10-22 00:00:00
---
The Zcash team has been hard at work preparing for the launch, which is on track for the 28th October. Despite some hiccups due to the <a class="reference external" href="https://www.wired.com/2016/10/internet-outage-ddos-dns-dyn/">widespread DNS disruptions</a> on Friday, today we deployed the fourth beta release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/milestone/42?closed=1">1.0.0-rc2</a>, to the testnet.

The new release includes the following user-visible changes:
<ol class="arabic simple">
 	<li>Wallet encryption has been disabled. The reasons for disabling this feature for the time being are explained in our <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0-rc2/doc/security-warnings.md#wallet-encryption">security warnings document</a>. We recommend using <a class="reference external" href="https://theintercept.com/2015/04/27/encrypting-laptop-like-mean/">full disk encryption</a> for now instead. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1552">#1552</a>)</li>
 	<li>We have included mitigations for security issues found by the NCC Group and Coinspect audits. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1459">#1459</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1464">#1464</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1504">#1504</a>)</li>
 	<li>We have merged some changes from Bitcoin to help address potential denial-of-service vulnerabilities. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1588">#1588</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1589">#1589</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1591">#1591</a>)</li>
 	<li>A bug that could cause assertion failures when restarting after a crash has been fixed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1378">#1378</a>)</li>
 	<li>A more efficient CPU Equihash solver written by John Tromp has been integrated into the built-in miner. This is not used by default, but can be enabled by adding <tt class="docutils literal">equihashsolver=tromp</tt> to <tt class="docutils literal">zcash.conf</tt>. Thanks go to John Tromp, and to @sarath-hotspot for providing the impetus for this improvement. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1570">#1570</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1578">#1578</a>)</li>
 	<li>Running the node now displays a screen showing node metrics (and some pretty ASCII art ☺). (<a class="reference external" href="https://github.com/zcash/zcash/pull/1375">#1375</a>)</li>
 	<li>The consensus rules have been tightened to reject block and transaction versions that were previously used by Bitcoin but are not valid for Zcash. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1556">#1556</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1600">#1600</a>)</li>
 	<li>The testnet now enforces the same rules on standard transactions as will be enforced on mainnet. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1582">#1582</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1557">#1557</a>)</li>
 	<li>We have made changes to the <tt class="docutils literal">getblocktemplate</tt> RPC call to support mining pools. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1424">#1424</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1602">#1602</a>)</li>
 	<li>Improved support for <a class="reference external" href="/deterministic-builds/">deterministic builds</a>. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1549">#1549</a>)</li>
 	<li>Build fixes for the musl C library used by Alpine Linux. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1558">#1558</a>)</li>
 	<li>Documentation improvements. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1500">#1500</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1575">#1575</a>)</li>
</ol>
For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/42?closed=1">1.0.0-rc2</a> release github milestone.

This release resets the beta testnet. It continues to use the beta 2 proving and verify keys.

To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.