---
ID: 4902
post_title: 'New Alpha Release: Mining Slow Start'
post_name: new-alpha-release-mining-slow-start
post_date: 2016-06-01 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-alpha-release-mining-slow-start/
published: true
tags:
  - alpha
  - mining
  - releases
categories:
  - General
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference<br />
implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z4">v0.11.2.z4</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple">
<li>We implemented a mining slow start to slowly ramp up the controlled currency supply after launch. (<a class="reference external" href="https://github.com/zcash/zcash/issues/762">#762</a>).</li>
<li>We enabled binary serialization (<a class="reference external" href="https://github.com/zcash/zcash/issues/954">#954</a>) and multicore zkSNARK computation in libsnark (<a class="reference external" href="https://github.com/zcash/zcash/issues/957">#957</a>) which provide performance improvements visible on our new <a class="reference external" href="https://speed.z.cash/comparison/?exe=1%2B9%2C1%2B25&amp;ben=7%2C2&amp;env=1&amp;hor=false&amp;bas=none&amp;chart=normal+bars">performance tracker</a>.</li>
<li>We added cryptographic binding of transactions using Ed25519 (<a class="reference external" href="https://github.com/zcash/zcash/issues/976">#976</a>).</li>
<li>We optimized the memory usage of our implementation of the Equihash proof of work (<a class="reference external" href="https://github.com/zcash/zcash/issues/921">#921</a>). The differences in running time and memory usage between the unoptimized and optimized versions are visualized <a class="reference external" href="https://speed.z.cash/comparison/?exe=1%2B9%2C1%2B25&amp;ben=9%2C4&amp;env=1&amp;hor=false&amp;bas=none&amp;chart=normal+bars">in this chart</a>.</li>
</ol>
<p>With mining slow start, the block reward linearly ramps up over a period of 5000 blocks before reaching its maximum value. This limits the effect of the "race to start", by providing a window after production launch during which the reward is low. Miners surprised by the launch will only be missing out on the low-value early blocks. Mining slow start was suggested by Jack Gavigan, one of our advisors.</p>
<p>As with our previous alpha releases, this resets our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/issues?q=milestone%3A%22Protocol+2016.0-beta%22+is%3Aclosed">Protocol 2016.0-beta</a> github milestone.</td>
</tr>
</tbody>
</table>
