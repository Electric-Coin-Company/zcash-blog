---
ID: 4915
post_title: 'New Release: 1.0.4'
post_name: new-release-1-0-4
post_date: 2016-12-15 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-1-0-4/
published: true
tags:
  - bugs
  - releases
  - sprout
  - zkSNARKs
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.4, which fixes several bugs, improves performance, and adjusts mining policies. With this release, private payments will get relayed and mined faster.</p>
<p>Summary of the changes in this release:</p>
<ol class="arabic simple">
<li>We fixed a cache invalidation bug that caused some orphaned blocks to trigger node crashes. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1928">#1928</a>)</li>
<li>We fixed a race condition that inhibited creation of multi-JoinSplit transactions. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1911">#1911</a>)</li>
<li>We adjusted mining policies to encourage inclusion of transactions containing JoinSplits. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1895">#1895</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1902">#1902</a>)</li>
<li>We improved rescan and reindex performance. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1892">#1892</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1904">#1904</a>)</li>
<li>We improved zk-SNARK verification performance by 7%. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1919">#1919</a>, <a class="reference external" href="https://speed.z.cash/comparison/?exe=1%2B208%2C1%2B226&amp;ben=3&amp;env=1&amp;hor=false&amp;bas=1%2B208&amp;chart=normal+bars">stats</a>)</li>
<li>We added additional well-formedness checks for JoinSplit proofs. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1938">#1938</a>)</li>
<li>We added a fee parameter to <cite>z_sendmany</cite>. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1907">#1907</a>)</li>
<li>We added a <cite>getlocalsolps</cite> RPC method for obtaining the mining rate without the metrics screen. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1642">#1642</a>)</li>
<li>The Bash completion files were updated to work with <cite>zcashd</cite>. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1909">#1909</a>)</li>
<li>The build scripts were extended to make porting Zcash to other platforms easier. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1905">#1905</a>)</li>
<li>A checkpoint was added at block height 15,000. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1865">#1865</a>)</li>
</ol>
<p>We're encouraging all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a> page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/48?closed=1">1.0.4</a> GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
