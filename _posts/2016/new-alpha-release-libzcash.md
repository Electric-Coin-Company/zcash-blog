---
ID: 4901
post_title: 'New Alpha Release: libzcash'
post_name: new-alpha-release-libzcash
post_date: 2016-05-17 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-alpha-release-libzcash/
published: true
tags:
  - alpha
  - cryptography
  - releases
  - zkSNARKs
categories:
  - General
---
<p>Today, we deployed a new alpha release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <a class="reference external" href="https://github.com/zcash/zcash/releases/tag/v0.11.2.z3">v0.11.2.z3</a>, to the testnet. The new release includes the following changes <a id="id1" class="footnote-reference" href="#id2">[1]</a>:</p>
<ol class="arabic simple">
<li>We've implemented the Zcash protocol in the form of libzcash, including a rewrite of our zkSNARK circuit. (<a class="reference external" href="https://github.com/zcash/zcash/issues/908">#908</a>)</li>
<li>We have a new implementation of our incremental merkle tree with better space efficiency and memory safety. (<a class="reference external" href="https://github.com/zcash/zcash/issues/889">#889</a>)</li>
<li>We've replaced crypto++'s key-private encryption with NoteEncryption as defined in our protocol specification. (<a class="reference external" href="https://github.com/zcash/zcash/issues/888">#888</a>)</li>
<li>We've added <a class="reference external" href="https://github.com/google/googletest">googletest</a> to our test suite for isolated unit testing of libzcash and other core components in our protocol. (<a class="reference external" href="https://github.com/zcash/zcash/issues/879">#879</a>)</li>
</ol>
<p>We've been hard at work solidifying a <a class="reference external" href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">protocol specification</a> which addresses security and terminology issues in the original Zerocash design, some of which we mentioned in <a class="reference external" href="/blog/fixing-zcash-vulns/">a previous blog post</a>. libzcash is a replacement for the old protocol implementation which brings us closer to realizing this new design.</p>
<p>As with our previous alpha releases, this resets our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Alpha-Guide">Public Alpha Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table id="id2" class="docutils footnote" frame="void" rules="none">
<colgroup>
<col class="label" />
<col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/issues?q=milestone%3A%22Protocol+2016.0-alpha-3+Implementation%22+is%3Aclosed">Zcash Protocol 2.0</a> github milestone.</td>
</tr>
</tbody>
</table>
