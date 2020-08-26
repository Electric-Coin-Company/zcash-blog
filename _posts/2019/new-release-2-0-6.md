---
ID: 8230
post_title: 'New Release: 2.0.6'
post_name: new-release-2-0-6
post_date: 2019-07-15 17:49:47
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-6/
published: true
tags:
  - bugs
  - releases
  - Sapling
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>This release of <code>zcashd</code> v2.0.6 is a maintenance release, focusing on code clean-ups and minor bug fixes. It precedes v2.0.7 which is planned to include the implementation of the Blossom upgrade for testnet.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This release will be supported until block 617512, expected to arrive around October 9th 2019, at which point the software will end-of-support halt and shut down.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1>Notable Changes in this Release</h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As of this release, Debian Stretch (v9) is fully supported for <code>zcashd</code>. While previous versions of <code>zcashd</code> worked with Stretch, this release marks full infrastructure support for the current version of Debian. If you are still running Debian Jessie (v8) for your <code>zcashd</code> environment, we highly recommend upgrading due to the increasing lack of support and security updates for Jessie. Please see our <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/install_debian_bin_packages.html#upgrading-debian-8-jessie-to-debian-9-stretch" target="_blank" rel="noopener noreferrer">documentation</a> on how to proceed. </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1>Summary of the Changes Included in this Release</h1>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>Debian Stretch is now a supported platform.</li>
<li>Fixed a bug in <code>z_mergetoaddress</code>, that prevented users sending from <code>ANY_SPROUT</code> or <code>ANY_SAPLING</code> when a wallet contained both Sprout and Sapling notes (<a href="https://github.com/zcash/zcash/pull/3910" target="_blank" rel="noopener noreferrer">#3910</a>)</li>
<li>Insight Explorer: we have been incorporating changes to support the Insight Explorer directly from <code>zcashd</code>. v2.0.6 includes the first change to an RPC method (<a href="https://github.com/zcash/zcash/pull/3863" target="_blank" rel="noopener noreferrer">#3863</a>)</li>
<li>Cherry-picked upstream improvements (<a href="https://github.com/zcash/zcash/pull/2912" target="_blank" rel="noopener noreferrer">#2912</a>)</li>
</ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>For a more complete list of changes, see our <a href="https://github.com/zcash/zcash/pulls?utf8=%E2%9C%93&amp;q=is%3Apr+milestone%3Av2.0.6+is%3Aclosed+" target="_blank" rel="noopener noreferrer">2.0.6</a> milestone.</p>
<!-- /wp:paragraph -->