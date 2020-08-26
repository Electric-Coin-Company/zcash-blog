---
ID: 4921
post_title: 'New Release: 1.0.9'
post_name: new-release-1-0-9
post_date: 2017-05-24 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-1-0-9/
published: true
tags:
  - bugs
  - performance
  - releases
  - scaling
  - sprout
  - testing
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.9. This is our first release using our new release cycle and focused exclusively on improvements to testing, security, benchmarking, automation, and portability.</p>
<p>This release is our first with the auto-deprecation feature described in our <a class="reference external" href="/blog/release-cycle-and-lifetimes/">Release Cycles and Lifetimes</a> post. It also introduces opt-in support for the <a class="reference external" href="https://www.amqp.org/">AMQP protocol</a>.</p>
<p>We encourage all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a> page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<ol class="arabic simple">
<li>Implemented automatic deprecation shutdown. <a class="reference external" href="https://github.com/zcash/zcash/pull/2297">#2297</a></li>
<li>Added opt-in AMQP support. <a class="reference external" href="https://github.com/zcash/zcash/pull/2189">#2189</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2362">#2362</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2280">#2280</a></li>
<li>Performance benchmarking and testing improvements: fix hang in benchmarking CI automation, add <cite>connectblockslow</cite> benchmark, re-enabled miner tests, improved error reporting in <cite>rpc-tests</cite> framework, changed default regtest port. <a class="reference external" href="https://github.com/zcash/zcash/pull/2397">#2397</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2372">#2372</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2389">#2389</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2376">#2376</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2265">#2265</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2270">#2270</a></li>
<li>Automated the release process, added build diagnostics for better user support, and fixed versioning problems in debian packaging and manpages. <a class="reference external" href="https://github.com/zcash/zcash/pull/2393">#2393</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2369">#2369</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2281">#2281</a></li>
<li>Added test for pairing bug when G1 is infinity. <a class="reference external" href="https://github.com/zcash/zcash/pull/2399">#2399</a></li>
<li>Documentation: Clarify release policy, added wallet backup instructions, and fixed some incorrect references to "bitcoin". <a class="reference external" href="https://github.com/zcash/zcash/pull/2401">#2401</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2340">#2340</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2364">#2364</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2338">#2338</a></li>
<li>Added alert sources for <a class="reference external" href="/blog/security-announcement-2017-04-13/">2017-04-13 security incident</a>. <a class="reference external" href="https://github.com/zcash/zcash/pull/2293">#2293</a></li>
</ol>
<p>In addition to improvements to the Zcash codebase itself, we made substantial improvements to our continuous integration (CI) system: we upgraded the Buildbot framework, modularized the CI code for easier maintenance, introduced a 'supported vs unsupported' build worker framework, repaired coverage analysis, and added new benchmarks.</p>
<p>These changes allow us to begin adding support for more platforms, to begin adding more benchmarks for judiciously selected optimization work, and to further improve the CI system with minimal disruption to future reference client releases.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/53?closed=1">1.0.9</a> GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>