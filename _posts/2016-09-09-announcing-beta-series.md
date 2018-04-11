---
ID: 1542
post_title: 'New Beta Release: Announcing the Zcash Beta Series'
author: Nathan Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/announcing-beta-series/
published: true
post_date: 2016-09-09 00:00:00
---
<p>Today, we deployed the first beta release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <cite>v1.0.0-beta1</cite>, to the testnet. This release, <cite>Beta 1</cite>, is the first release of the Zcash <cite>Beta Series</cite> and represents a new phase of development.</p>
<p><em>Note: the official Zcash currency is non-existent until our October 28th launch. Only testnet coins exist and they carry no value.</em></p>
<div class="section" id="zcash-beta-series">
<h2>Zcash Beta Series</h2>
<p>The Beta series is the final phase of development prior to the launch of Zcash 1.0.0, which begins the <a class="reference external" href="/sprout-roadmap/">Sprout Series</a>. The Beta Series is notably different from our earlier alpha releases in several ways:</p>
<ul class="simple"><li>We're using a new versioning scheme, the first beta release is <cite>v1.0.0-beta1</cite>, the next <cite>v1.0.0-beta2</cite> and so on.</li>
<li>Starting with <cite>v1.0.0-beta1</cite> the new high level <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0-beta1/doc/payment-api.md">RPC interface</a> is in place. The early RPC interface is deprecated and will be removed.</li>
<li>Only high priority changes will be merged, including: important security mitigations, fixing bugs which inhibit basic operation, improving build, packaging, and documentation, and changes for production infrastructure.</li>
</ul><p>As we approach our target 1.0 Sprout launch date of October 28th, 2016, we'll release several Beta versions. During this time we'll be working with partners and community members to integrate Zcash into more tools, products, and services.</p>
<p><em>The Zcash Beta Series is a good time for integration work for third party services and products interested in deploying Zcash support.</em></p>
<p>As the Beta Series matures, we'll enter a <cite>pre-release phase</cite> during which we'll publish several essential items:</p>
<ul class="simple"><li>security audit reports</li>
<li>proof-of-work analysis</li>
<li>source code and security proof of our secure parameter setup</li>
<li>securely generated parameters</li>
</ul><p>Stay tuned for those publications.</p>
</div>
<div class="section" id="about-beta-1-release">
<h2>About Beta 1 release</h2>
<p>Today we've released Zcash Beta 1, aka <cite>v1.0.0-beta1</cite>. Building on the <a class="reference external" href="/new-alpha-release-solidifying-the-consensus-protocol/">previous alpha release</a> which finalized consensus changes (unless we discover critical flaws) this release adds the new high level <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0-beta1/doc/payment-api.md">RPC interface</a>. The <cite>v1.0.0-beta1</cite> release includes these major changes:</p>
<ul class="simple"><li>Wallet support for the high-level interface, including detecting received notes, selecting notes for transfers, listing transactions, getting balances, and calculating block subsidies. See <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0-beta1/doc/payment-api.md">RPC interface</a>. [<a class="reference external" href="https://github.com/zcash/zcash/pull/1355">#1355</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1323">#1323</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1315">#1315</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1233">#1233</a>]</li>
<li>We rolled back a "stable txid" feature intended to fix malleability issues, see <a class="reference external" href="/metamorphosis-of-malleable-transactions/">our post about the rollback</a>. [<a class="reference external" href="https://github.com/zcash/zcash/pull/1316">#1316</a>]</li>
<li>We tweaked the difficulty adjustment algorithm. [<a class="reference external" href="https://github.com/zcash/zcash/pull/1338">#1338</a>]</li>
<li>Several other security and other bug fixes and cleanups, full details on the <a class="reference external" href="https://github.com/zcash/zcash/milestone/28?closed=1">Beta 1 github milestone</a>.</li>
</ul><p><strong>Caution:</strong> In the interest of getting user feedback we're releasing <cite>v1.0.0-beta1</cite> today even though it lacks the same level of automated test coverage as our core consensus code. Future releases in the Beta series will focus on improving test coverage as well as discovering and fixing bugs.</p>
<p>Additionally, every release moving forward will contain a document with security warnings. For this release, see <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0-beta1/doc/security-warnings.md">security-warnings.md</a>. <strong>Important:</strong> Please also regularly check out website for security issues discovered after a release is deployed to users.</p>
</div>
<div class="section" id="stay-involved">
<h2>Stay Involved</h2>
<p>Try out the Beta series releases by following the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Beta-Guide">Beta Guide</a>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the github project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when Zcash <a class="reference external" href="/sprout-roadmap/">Sprout Series</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>. We tweet <a class="reference external" href="https://twitter.com/zcashco">@ZcashCo</a>.</p>
</div>