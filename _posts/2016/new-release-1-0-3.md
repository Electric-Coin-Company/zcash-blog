---
ID: 4914
post_title: 'New Release: 1.0.3'
post_name: new-release-1-0-3
post_date: 2016-11-17 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-1-0-3/
published: true
tags:
  - bugs
  - releases
  - sprout
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.3 which fixes several crashes and security bugs, improves performance, and adjusts relay policies.</p>
<p>We strongly recommend users and miners update to this version, as it fixes a cache invalidation bug that could be used by an attacker to disrupt the network. (See <a class="reference external" href="https://github.com/zcash/zcash/pull/1874">#1874</a>.)</p>
<p>Other changes in this release include:</p>
<ol class="arabic simple">
<li>We fixed a bug that caused the wallet to crash during startup in some situations, such as when the wallet is not synchronized properly with the blockchain. (<a class="reference external" href="https://github.com/zcash/zcash/issues/1858">#1858</a>)</li>
<li>We re-enabled note randomization that was temporarily disabled in 1.0.2. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1814">#1814</a>)</li>
<li>We adjusted fee policies to reflect changes made in Bitcoin Core and encourage relaying of transactions containing JoinSplits. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1855">#1855</a>)</li>
<li>We improved diagnostics and strengthened testing for the merkle tree's interaction with the constraint system. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1797">#1797</a>)</li>
<li>We disabled RPC keepalive features temporarily to avoid deadlocks. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1847">#1847</a>)</li>
<li>We adjusted our use of the libsnark verification API to improve zk-SNARK verification performance by 10%. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1760">#1760</a>, <a class="reference external" href="https://speed.z.cash/changes/?rev=057ab6b4d1&amp;exe=undefined&amp;env=1">stats</a>)</li>
<li>We changed the error message format for <cite>z_sendmany</cite> so that amounts are displayed in units of ZEC. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1838">#1838</a>)</li>
</ol>
<p>We're encouraging all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a> page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/47?closed=1">1.0.3</a> github milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
