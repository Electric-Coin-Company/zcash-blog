---
ID: 4904
post_title: 'New Alpha Release: Solidifying the Consensus Protocol'
post_name: >
  new-alpha-release-solidifying-the-consensus-protocol
post_date: 2016-08-25 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-alpha-release-solidifying-the-consensus-protocol/
published: true
tags:
  - alpha
  - consensus
  - encrypted memo field
  - releases
  - security audits
categories:
  - General
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z9">v0.11.2.z9</a>, to the testnet. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple">
<li>Decreased block header size to address a bug interfering with the testnet (<a class="reference external" href="https://github.com/zcash/zcash/pull/1289">#1289</a>).</li>
<li>Ensured that Zcash secrets are saved along with Bitcoin secrets in wallets (<a class="reference external" href="https://github.com/zcash/zcash/pull/1198">#1198</a>).</li>
<li>Implemented more space-efficient encodings for Equihash solutions (<a class="reference external" href="https://github.com/zcash/zcash/pull/1175">#1175</a>).</li>
<li>Implemented more space-efficient encodings for zk-SNARK proofs following an IEEE standard (<a class="reference external" href="https://github.com/zcash/zcash/pull/1262">#1262</a>).</li>
<li>Increased the size of the memo field sent with notes, to 512 bytes (<a class="reference external" href="https://github.com/zcash/zcash/pull/1187">#1187</a>).</li>
<li>Merged in upstream Bitcoin patches related to Denial-of-Service protection (<a class="reference external" href="https://github.com/zcash/zcash/pull/1251">#1251</a>).</li>
<li>Implemented the first stages of adding a new higher-level RPC interface so that clients don't have to deal with details of the underlying cryptographic protocol (<a class="reference external" href="https://github.com/zcash/zcash/issues/701">#701</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/756">#756</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1197">#1197</a>).</li>
<li>Began addressing issues found by NCC Group as part of our <a class="reference external" href="/blog/auditing-zcash/">security audits</a> (<a class="reference external" href="https://github.com/zcash/zcash/pull/1214">#1214</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1215">#1215</a>).</li>
</ol>
<p>We do not expect to make any other changes to the consensus protocol, except for possible security fixes, until after 1.0.</p>
<p>This alpha release will reset our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To<br />
get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address<br />
<a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestone/27?closed=1">z9 release</a> github milestone.</td>
</tr>
</tbody>
</table>
