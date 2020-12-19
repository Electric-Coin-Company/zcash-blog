---
ID: 4905
post_title: 'New Alpha Release: Terminology and Security'
post_name: >
  new-alpha-release-terminology-and-security
post_date: 2016-07-22 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-alpha-release-terminology-and-security/
published: true
tags:
  - alpha
  - releases
categories:
  - General
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z7">v0.11.2.z7</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple">
<li>The terminology of the RPC and internal code has been modified to reflect our<br />
protocol specification. (<a class="reference external" href="https://github.com/zcash/zcash/issues/1090">#1090</a>)</li>
<li>We have forked libsnark and made a number of changes to improve security and performance. The public parameters have shrunk by about 35% and memory usage during JoinSplit creation has <a class="reference external" href="https://speed.z.cash/timeline/?exe=1&amp;base=1%2B9&amp;ben=memory+createjoinsplit&amp;env=1&amp;revs=50&amp;equid=off&amp;quarts=on&amp;extr=on">improved</a> by several hundred megabytes. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1104">#1104</a>)</li>
<li>We have published guidelines about side-channel attacks and other security warnings.</li>
<li>The alert key has been changed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1105">#1105</a>)</li>
<li>A bug in the difficulty adjustment algorithm has been fixed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1124">#1124</a>)</li>
</ol>
<p>We have changed protocol version numbers, which requires all old nodes to upgrade to continue to use the testnet network. However, we are not resetting the testnet blockchain for this release.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestone/26?closed=1">z7 release</a> github milestone.</td>
</tr>
</tbody>
</table>
