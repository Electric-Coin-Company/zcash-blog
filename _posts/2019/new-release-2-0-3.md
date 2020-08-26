---
ID: 6802
post_title: 'New Release: 2.0.3'
post_name: new-release-2-0-3
post_date: 2019-02-14 13:29:26
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-3/
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
<p>This release is intended to address security issues in libraries used by Zcash and other outstanding tickets that were in our Spring cleaning sprints.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Notable Changes in this Release</h2>
<!-- /wp:heading -->
<!-- wp:heading {"level":3} -->
<h3>[CVE-2019-6250] Update libzmq version</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>A pointer overflow, with code execution, was discovered in ZeroMQ libzmq (aka 0MQ) 4.2.x and 4.3.x before 4.3.1. A&nbsp;<code>v2_decoder.cpp zmq::v2_decoder_t::size_ready</code>&nbsp;integer overflow allows an authenticated attacker to overwrite an arbitrary amount of bytes beyond the bounds of a buffer, which can be leveraged to run arbitrary code on the target system. This update addresses the vulnerability when ZeroMQ is enabled, which is not enabled by default.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>Bitcoin 0.12 Performance Improvements</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>This change makes sigcache faster, more efficient, and larger. It also reduces the number of database lookups when processing new transactions.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Summary of the Changes Included in this Release</h2>
<!-- /wp:heading -->
<!-- wp:list {"ordered":true} -->
<ol><li>Update ZMQ to 4.3.1 (<a href="https://github.com/zcash/zcash/pull/3789">#3789</a>)</li><li>Fix Tx expiring soon test (<a href="https://github.com/zcash/zcash/pull/3784">#3784</a>)</li><li>ZMQ: add flag to publish all checked blocks (<a href="https://github.com/zcash/zcash/pull/3737">#3737</a>)</li><li>wallet: Skip transactions with no shielded data in CWallet::SetBestChain() (<a href="https://github.com/zcash/zcash/pull/3711">#3711</a>)</li><li>Update z_mergetoaddress documentation (<a href="https://github.com/zcash/zcash/pull/3699">#3699</a>)</li><li>Allow user to ask server to save the Sprout R1CS to a file during startup (<a href="https://github.com/zcash/zcash/pull/3691">#3691</a>)</li><li>On shutdown, wait for miner threads to exit (join them) (<a href="https://github.com/zcash/zcash/pull/3647">#3647</a>)</li><li>Update for Mac OS local rpc-tests</li><li>Bitcoin 0.12 performance improvements (<a href="https://github.com/zcash/zcash/pull/3263">#3263</a>)</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>For a more complete list of changes, please see the&nbsp;<a href="https://github.com/zcash/zcash/pulls?q=is%3Apr+milestone%3Av2.0.3+is%3Aclosed">2.0.3</a>&nbsp;milestone.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For information on specific Sapling RPC parameter changes, please see the&nbsp;<a href="https://zcash.readthedocs.io/en/latest/rtd_pages/nu_dev_guide.html#using-zcashd-unmodified">Network Upgrade Developer guide</a>.</p>
<!-- /wp:paragraph -->