---
ID: 1579
post_title: 'New Alpha Release: Faster Block Times'
author: Taylor Hornby
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-alpha-release-faster-block-times/
published: true
post_date: 2016-06-17 00:00:00
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z5">v0.11.2.z5</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple"><li>The block interval target has been decreased to 2.5 minutes, without changing the monetary supply curve (<a class="reference external" href="https://github.com/zcash/zcash/pull/989">#989</a>).</li>
<li>The difficulty adjustment has been changed to one based on DigiShield v3/v4 (<a class="reference external" href="https://github.com/zcash/zcash/issues/147">#147</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1004">#1004</a>).</li>
<li>Coinbase rewards must be protected before they can be used in transparent transactions (<a class="reference external" href="https://github.com/zcash/zcash/pull/1017">#1017</a>).</li>
<li>Upstream's soft forking rules now apply unconditionally to all blocks from the start (<a class="reference external" href="https://github.com/zcash/zcash/pull/1016">#1016</a>).</li>
<li>The Equihash implementation has been optimized further (<a class="reference external" href="https://github.com/zcash/zcash/pull/988">#988</a>), enabling us to switch to more difficult (higher memory) parameters (<a class="reference external" href="https://github.com/zcash/zcash/pull/1003">#1003</a>). The difference can be seen <a class="reference external" href="https://speed.z.cash/comparison/?exe=1%2B25%2C1%2B43&amp;ben=9%2C4&amp;env=1&amp;hor=false&amp;bas=none&amp;chart=normal+bars">on our performance tracker</a>.</li>
<li>The <tt class="docutils literal"><span class="pre">-relaypriority</span></tt> default has been set to <tt class="docutils literal">false</tt>, to enable spending of low-value rewards during mining slow start (<a class="reference external" href="https://github.com/zcash/zcash/pull/1001">#1001</a>).</li>
<li>The note commitment tree depth has been increased from 20 to 29 (<a class="reference external" href="https://github.com/zcash/zcash/pull/994">#994</a>). The resulting increase in memory usage when creating a JoinSplit is visible <a class="reference external" href="https://speed.z.cash/comparison/?exe=1%2B25%2C1%2B43&amp;ben=7%2C2&amp;env=1&amp;hor=false&amp;bas=none&amp;chart=normal+bars">here</a>.</li>
<li>Zcash addreses and spending keys are now encoded with Base58Check (<a class="reference external" href="https://github.com/zcash/zcash/pull/1026">#1026</a>).</li>
</ol><p>As with our previous alpha releases, this resets our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none"><colgroup><col class="label"/><col/></colgroup><tbody valign="top"><tr><td class="label"><a class="fn-backref" href="#id1">[1]</a></td><td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/issues?q=milestone%3A%22Protocol+2016.1+Implementation%22+is%3Aclosed">Protocol 2016.1 Implementation</a> github milestone.</td></tr></tbody></table>