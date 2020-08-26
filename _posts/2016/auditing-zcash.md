---
ID: 4869
post_title: Auditing Zcash
post_name: auditing-zcash
post_date: 2016-08-17 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/auditing-zcash/
published: true
tags:
  - cryptography
  - security
  - security audits
categories:
  - General
---
<p>Our <a class="reference external" href="/blog/helloworld/">mission</a> is to make the first open financial technology with zero-knowledge privacy, for every person in the world to use. To that end we are commissioning multiple security audits and design evaluations, and will publish the results in full.</p>
<div class="section" id="audit-strategy">
<h2>Audit Strategy</h2>
<p>Zcash combines novel cryptography with blockchain consensus, and <a class="reference external" href="https://github.com/zcash/zcash">our reference implementation</a> is a C++ networking application. Our auditing strategy is to engage experts with different specializations to focus on different aspects of the system, including: cryptography, cryptocurrency (esp. Bitcoin), C++, networking, and traditional application security.</p>
</div>
<div class="section" id="auditors-and-consultants">
<h2>Auditors and Consultants</h2>
<p>Given our strategy, we've initiated two audits and one design analysis with leading experts in different areas. Each consultant will have their own distinct scope and focus, which will be clearly delineated in their respective reports.</p>
<p><a class="reference external" href="https://www.nccgroup.trust/us/">NCC Group</a> - From working alongside NCC Group as the <a class="reference external" href="https://leastauthority.com">Least Authority</a> auditing team, we were impressed with their abilities as skilled security auditors for cryptographic software.</p>
<p><a class="reference external" href="https://coinspect.com/">Coinspect</a> - When we wanted to find cryptocurrency specialists, Coinspect quickly came to mind. They've published many innovative protocol designs, as well as insightful analyses.</p>
<p><a class="reference external" href="https://en.wikipedia.org/wiki/Solar_Designer">Solar Designer</a> - We chose Solar Designer because he is a famous <a class="reference external" href="http://phrack.org/issues/69/2.html">old school hacker</a>, developed return to libc (ret2libc), which started the move from injected code (shellcode) to borrowed code, and developed the first generic heap-based buffer overflow exploitation technique (by<br />
attacking "unlink", an operation that coalesces adjacent chunks when an<br />
allocation is freed).</p>
<p>We are proud to work with teams that, like us, value open source, and aim to create accessible and secure systems for everyone.</p>
</div>
<div class="section" id="scope">
<h2>Scope</h2>
<p>We are focusing our audits on specific components:</p>
<ul class="simple">
<li>zkSNARK cryptography (eg: libsnark)</li>
<li>Zcash cryptographic construction (our "zk-SNARK circuit")</li>
<li>Proof of Work algorithm - Equihash</li>
<li>Consensus changes (from Bitcoin)</li>
<li>Specification adherence</li>
<li>C++, race conditions, networking, buffer overflows, dependency management</li>
</ul>
<p>We have a limited budget and schedule so we must be selective in our focus. In selecting the audit scope, we're relying on a few assumptions that we believe mitigate security risk:</p>
<ul class="simple">
<li>Bitcoin Core has survived for ~7 years, controlling billions of dollars worth of funds and is thus well tested in the wild. We will focus primarily on our changes from Bitcoin, although we are doing some auditing for memory safety problems in code that hasn't changed from Bitcoin Core and its dependencies.</li>
<li>The zkSNARK cryptographic technique is peer reviewed, so we won't look for breakthroughs there.</li>
<li>We use only a subset of libsnark, so we'll ignore the parts we don't use <a class="footnote-reference" href="#id2" id="id1">[1]</a>.</li>
<li>The Zcash circuit is modified from the peer-reviewed Zerocash circuit, so we will focus more on the changes than the whole construction.</li>
</ul>
</div>
<div class="section" id="schedule">
<h2>Schedule</h2>
<p>The first audits have already begun, and we may schedule future audits to gain further confidence in our security at launch. With proper and thorough auditing the aim is to mitigate all vulnerabilities and lessen risk--this thoroughness is one reason for our launch delay. We described this schedule change in our <a class="reference external" href="/blog/zcash-launch-and-roadmap/">Zcash Sprout Launch post</a>.</p>
</div>
<div class="section" id="understanding-risk">
<h2>Understanding Risk</h2>
<p>For an open, permissionless system to be viable, users must be able to justifiably rely on its security and robustness. Ensuring that this  a daunting task. The best service we can provide for potential users of Zcash is to ensure they understand the associated risks as well as possible.</p>
<p>Security audits and algorithm analyses are not guarantees of safety or correct operation. Each consultant is focused on a specific kind of analysis and cannot vouch for the entire system, nor do they necessarily endorse Zcash as a whole.</p>
</div>
<div class="section" id="conclusion">
<h2>Conclusion</h2>
<p>Zcash is based on peer-reviewed cryptographic research, and built by a security-specialized engineering team on an open source platform based on Bitcoin Core's battle-tested codebase. Publishing multiple security audits is yet another example of our best effort at deploying a system designed to withstand the demands of world-wide financial infrastructure.</p>
<p>— Nathan Wilcox, 2016-08-17</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>We have created a libsnark fork which removed portions unused by Zcash.</td>
</tr>
</tbody>
</table>
</div>
