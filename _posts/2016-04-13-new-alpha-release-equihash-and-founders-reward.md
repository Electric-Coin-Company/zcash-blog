---
ID: 1578
post_title: 'New Alpha Release: Equihash and Founders&#8217; Reward'
author: Taylor Hornby
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-alpha-release-equihash-and-founders-reward/
published: true
post_date: 2016-04-13 00:00:00
---
Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z2">v0.11.2.z2</a>, to the testnet. The new release includes the following changes <a id="id1" class="footnote-reference" href="/new-alpha-release-equihash-and-founders-reward/#id2">[1]</a>:
<ol class="arabic simple">
 	<li>We've added the <a class="reference external" href="https://www.internetsociety.org/sites/default/files/blogs-media/equihash-asymmetric-proof-of-work-based-generalized-birthday-problem.pdf">Equihash</a> proof-of-work for block mining (<a class="reference external" href="https://github.com/zcash/zcash/issues/27">#27</a>).</li>
 	<li>We've implemented the Founders' Reward as described in <a class="reference external" href="/funding/">our funding post</a> (<a class="reference external" href="https://github.com/zcash/zcash/issues/125">#125</a>).</li>
 	<li>We've added a performance measurement system to improve performance in future releases (<a class="reference external" href="https://github.com/zcash/zcash/issues/748">#748</a>).</li>
</ol>
Equihash is a Proof-of-Work algorithm devised by Dmitry Khovratovich and Alex Biryukov. It relies on RAM as the bottleneck resource for generating proofs and we believe this makes it ASIC resistant. We'll post soon with more detail on our motivations, algorithm selection, and implementation. This release uses temporary proof-of-concept parameters and an unoptimized implementation.

This release breaks compatibility with the old testnet. Several of our upcoming releases will also break compatibility because we'll be adjusting each of these features as we move forward, such as <a class="reference external" href="https://github.com/zcash/zcash/issues/762">#762</a> <em>Mining Slow Start</em>, <a class="reference external" href="https://github.com/zcash/zcash/issues/856">#856</a> <em>Select Equihash Parameters</em>, and <a class="reference external" href="https://github.com/zcash/zcash/issues/857">#857</a> <em>Optimize Equihash Implementation</em>.

To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.
<table id="id2" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestones/PoW%20Release">PoW Release</a> github milestone.</td>
</tr>
</tbody>
</table>