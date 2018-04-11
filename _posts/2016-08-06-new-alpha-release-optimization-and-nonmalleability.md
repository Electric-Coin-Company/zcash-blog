---
ID: 1582
post_title: 'New Alpha Release: Optimization and Non-malleability'
author: Simon Liu
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-alpha-release-optimization-and-nonmalleability/
published: true
post_date: 2016-08-06 00:00:00
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z8">v0.11.2.z8</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple"><li>Equihash mining parameters have been adjusted to n=200, k=9 to reduce average solution search time to &lt;45 seconds, and average time-to-first-solution to &lt;30 seconds. (<a class="reference external" href="https://github.com/zcash/zcash/issues/856">#856</a>)</li>
<li>The Equihash miner will now interrupt and cancel an existing solution search when a new valid block arrives. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1055">#1055</a>)</li>
<li>The Equihash miner will now check solutions as soon as they are found. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1143">#1143</a>)</li>
<li>Transaction malleability has been fixed so that valid transactions can not be modified in-flight. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1144">#1144</a>)</li>
<li>The SIGHASH_SINGLE bug has been fixed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1078">#1078</a>)</li>
<li>Compilation flags have been updated to harden security. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1064">#1064</a>)</li>
</ol><p>The zcraw* RPC commands are still available for use but will be deprecated in a future release.</p>
<p>This alpha release will reset our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none"><colgroup><col class="label"/><col/></colgroup><tbody valign="top"><tr><td class="label"><a class="fn-backref" href="#id1">[1]</a></td><td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestone/36?closed=1">z8 release</a> github milestone.</td></tr></tbody></table>