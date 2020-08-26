---
ID: 5740
post_title: 'New Release: 2.0.2'
post_name: new-release-2-0-2
post_date: 2018-12-04 07:00:19
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-2/
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
<p>This release adds further support for Sapling in the zcashd wallet RPC and mitigates an issue identified by an external auditor. Information on the Sapling network upgrade (which activated on Oct 28th 2018) can be found below:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li><a href="https://z.cash/upgrade/sapling.html">Sapling Network Upgrade</a></li><li><a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html">Sapling Turnstile</a></li><li><a href="https://zcash.readthedocs.io/en/latest/rtd_pages/nu_dev_guide.html">Network Upgrade Dev Guide</a></li></ul>
<!-- /wp:list -->
<!-- wp:heading -->
<h2>Notable Changes in this Release</h2>
<!-- /wp:heading -->
<!-- wp:heading {"level":3} -->
<h3>RPC&nbsp;<code>z_getnewaddress</code>&nbsp;now returns a Sapling address by default</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Previously when calling&nbsp;<code>z_getnewaddress</code>&nbsp;a Sprout shielded address would be returned by default. With this release, a Sapling shielded address will be returned by default.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>RPC <code>z_mergetoaddress</code> is now Sapling ready</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The <code>z_mergetoaddress</code> call is now supported by Sapling shielded addresses. This call remains an experimental feature so to enable it, users must restart zcashd with the <code>-experimentalfeatures</code> and<br /><code>-zmergetoaddress</code> commandline options, or add these two lines<br />to the zcash.conf file:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>experimentalfeatures=1</li><li>zmergetoaddress=1</li></ul>
<!-- /wp:list -->
<!-- wp:heading {"level":3} -->
<h3>Transactions expiring soon will not be propagated</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>To address auditor issue ZEC-013 which identified a potential denial-of-service vector related to expiry height, nodes will no longer propagate transactions which are expiring soon, defined as within the next 3 blocks. For example, if the current block height is 99, and the next block to be mined is 100, a transaction with an expiry height of 100, 101, 102 will be considered "expiring soon" and will be rejected by the mempool. A transaction with an expiry height of 103 will be accepted. This does not impact transactions which have disabled expiry height (by setting to 0).</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>New Signing Key</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Users upgrading to 2.0.2 via the Debian package will need to get the new signing key.&nbsp;</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>If you see a message about the package being unauthenticated or unverifiable, including:</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><code>The following signatures couldn't be verified because the public key is not available: NO_PUBKEY C2A798EF998940FA&nbsp;</code></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Do not upgrade anyway if prompted. Instead, follow the guide found in the <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/install_debian_bin_packages.html">Debian Binary Package Setup docs</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Summary of the Changes Included in this Release</h2>
<!-- /wp:heading -->
<!-- wp:list {"ordered":true} -->
<ol><li>Add Sapling support to RPC&nbsp;<code>z_mergetoaddress</code>&nbsp;(<a href="https://github.com/zcash/zcash/pull/3619">#3619</a>)</li><li>Mitigate ZEC-013 transaction expiry height related DoS vector (<a href="https://github.com/zcash/zcash/pull/3689">#3689</a>)</li><li>Return Sapling addresses by default when calling RPC&nbsp;<code>z_getnewaddress</code>&nbsp;(<a href="https://github.com/zcash/zcash/pull/3680">#3680</a>)</li><li>Add Sapling spend and output description benchmarks to RPC&nbsp;<code>zcbenchmark</code>&nbsp;(<a href="https://github.com/zcash/zcash/pull/3611">#3611</a>)</li><li>Fix bug with Sapling chain value tracking (<a href="https://github.com/zcash/zcash/pull/3684">#3684</a>)</li><li>Fix encoding bug with non-ASCII parameter paths, primarily affecting Windows (<a href="https://github.com/zcash/zcash/pull/3633">#3633</a>)</li><li>Backport from upstream the relaying of blocks when pruning (<a href="https://github.com/zcash/zcash/pull/2815">#2815</a>)</li><li>Don't ban peers when loading pre-Sapling blocks during syncing (<a href="https://github.com/zcash/zcash/pull/3670">#3670</a>)</li><li>Fix bug with contents of default memo in Sapling (<a href="https://github.com/zcash/zcash/pull/3605">#3605</a>)</li><li>Update tests for Sapling (<a href="https://github.com/zcash/zcash/pull/3585">#3585</a>,&nbsp;<a href="https://github.com/zcash/zcash/pull/3588">#3588</a>)</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>For a more complete list of changes, please see the&nbsp;<a href="https://github.com/zcash/zcash/milestone/76?closed=1">2.0.2</a>&nbsp;milestone.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For information on specific Sapling RPC parameter changes, please see the&nbsp;<a href="https://zcash.readthedocs.io/en/latest/rtd_pages/nu_dev_guide.html#using-zcashd-unmodified">Network Upgrade Developer guide</a>.</p>
<!-- /wp:paragraph -->