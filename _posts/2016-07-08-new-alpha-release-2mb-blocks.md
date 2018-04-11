---
ID: 1577
post_title: 'New Alpha Release: 2MB blocks'
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-alpha-release-2mb-blocks/
published: true
post_date: 2016-07-08 00:00:00
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z6">v0.11.2.z6</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple"><li>The block size limit has been increased to 2MB. (<a class="reference external" href="https://github.com/zcash/zcash/issues/765">#765</a>) We're tracking the worst-case verification costs in <a class="reference external" href="https://speed.z.cash/timeline/?exe=1&amp;base=1%2B9&amp;ben=time+validatelargetx&amp;env=1&amp;revs=10&amp;equid=off&amp;quarts=on&amp;extr=on">some new performance measurements</a> and in <a class="reference external" href="https://github.com/zcash/zcash/issues/1077">#1077</a> in
order to mitigate potential DoS attacks.</li>
<li>Equihash nonces are now randomized to avoid duplicate effort by miners. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1060">#1060</a>)</li>
<li>Equihash solving runs are now slightly more efficient. See <a class="reference external" href="https://github.com/zcash/zcash/pull/1049">#1049</a> and the <a class="reference external" href="https://speed.z.cash/timeline/?exe=1&amp;base=1%2B9&amp;ben=time+solveequihash&amp;env=1&amp;revs=10&amp;equid=off&amp;quarts=on&amp;extr=on">change in performance measurements</a> on our tracker.</li>
</ol><p>Unlike previous alpha releases, we have not reset the testnet in order to give our <a class="reference external" href="/new-alpha-release-mining-slow-start/">mining slow start</a> more time to run. Therefore, the block size limit change has been introduced as a (naive) hardfork.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none"><colgroup><col class="label"/><col/></colgroup><tbody valign="top"><tr><td class="label"><a class="fn-backref" href="#id1">[1]</a></td><td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/issues?q=milestone%3A%22Consensus+Parameter+Tuning+%2F+Optimization%22+is%3Aclosed">Consensus Parameter Tuning / Optimization</a> github milestone.</td></tr></tbody></table>