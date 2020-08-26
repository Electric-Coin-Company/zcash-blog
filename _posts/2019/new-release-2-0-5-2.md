---
ID: 7562
post_title: 'New Release: 2.0.5-2'
post_name: new-release-2-0-5-2
post_date: 2019-05-21 11:05:58
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-5-2/
published: true
tags:
  - bugs
  - consensus
  - migration tool
  - releases
  - Sapling
  - sprout
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p><strong>Note</strong>: This release of Zcashd v2.0.5-2 is a hotfix release that all users are encouraged to upgrade to, especially users who built v2.0.5 or v2.0.5-1 from source. We became aware of issues in the Sprout-to-Sapling migration tool in these two prior versions. Zcashd v2.0.5-2 fixes the issues. Users who normally upgrade via Debian package repository or tarball download were not exposed to v2.0.5 or  v2.0.5-1.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The v2.0.5 release added the Sprout-to-Sapling migration tool, introduced a new consensus rule on mainnet to reject blocks that violate turnstiles and adds 64-bit ARMv8 support. Zcashd v2.0.5-2 will be supported until block 598012, expected to arrive around 05 September 2019, at which point the software will end-of-support halt and shut down.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Notable Changes</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Sprout-to-Sapling Migration Tool</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release includes the addition of a tool that will enable users to migrate shielded funds from the Sprout pool to the Sapling pool while minimizing information leakage.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The migration can be enabled using the RPC&nbsp;<code>z_setmigration</code>&nbsp;or by including&nbsp;<code>-migration</code>&nbsp;in the&nbsp;<code>zcash.conf</code>&nbsp;file. Unless otherwise specified funds will be migrated to the wallet's default Sapling address; it is also possible to set the receiving Sapling address using the&nbsp;<code>-migrationdestaddress</code>&nbsp;option in&nbsp;<code>zcash.conf</code>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>See the <a href="/blog/sprout-to-sapling-migration-tool">blog post</a>, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html#migration-tool" target="_blank">documentation</a> and <a href="https://github.com/zcash/zips/blob/master/zip-0308.rst" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP 308</a> for more details.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sprout-to-Sapling Migration Tool Fixes </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The 2.0.5-1 and 2.0.5-2 releases include fixes to the Sprout to Sapling<br>
Migration Tool found in testing.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>New consensus rule: Reject blocks that violate turnstile</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In the 2.0.4 release, the consensus rules were changed on testnet to enforce a new rule which marks blocks as invalid if they would lead to a turnstile violation in the Sprout or Shielded value pools. <strong>This release enforces the consensus rule change on mainnet.</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The motivations and deployment details can be found in <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/blob/master/zip-0209.rst" target="_blank">ZIP 209</a> and <a href="https://github.com/zcash/zcash/pull/3968" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3968</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Developers can use a new experimental feature&nbsp;<code>-developersetpoolsizezero</code>&nbsp;to test Sprout and Sapling turnstile violations. See&nbsp;<a href="https://github.com/zcash/zcash/pull/3964" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3964</a>&nbsp;for more details.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>64-bit ARMv8 support</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Added ARMv8 (AArch64) support. This enables users to build zcash on even more devices.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For information on how to build see the <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/user_guide.html#build" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">User Guide</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Users on the Zcash forum have reported successes with both the Pine64 Rock64Pro and Odroid C2, which contain 4GB and 2GB of RAM respectively.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Just released, the Odroid N2 looks like a great solution with 4GB of RAM. The newly released Jetson Nano Developer Kit from Nvidia (also 4GB of RAM) is also worth a look. The NanoPC-T3 Plus is another option but for the simplest/best experience choose a board with 4GB of RAM. Just make sure before purchase that the CPU supports the 64-bit ARMv8 architecture.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Summary of the Changes</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>v2.0.5</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Sprout-to-Sapling migration (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3848" target="_blank">#3848</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3888" target="_blank">#3888</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3967" target="_blank">#3967</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3973" target="_blank">#3973</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3977" target="_blank">#3977</a>)</li><li>Activate turnstile on mainnet (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3968" target="_blank">#3968</a>)</li><li>Update boost to v1.70.0 to eliminate build warning (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3951" target="_blank">#3951</a>)</li><li>Fix new HD seed generation for previously-encrypted wallets (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3940" target="_blank">#3940</a>)</li><li>Fix enable-debug build DB_COINS undefined (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3907" target="_blank">#3907</a>)</li><li>Update "Zcash Company" to "Electric Coin Company" (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3901" target="_blank">#3901</a>)</li><li>Support additional cross-compilation targets in Rust (<a href="https://github.com/zcash/zcash/pull/3505" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3505</a>)</li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>v2.0.5-1</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>We fixed an issue that would cause the Zcashd to crash when calling&nbsp;<code>z_getmigrationstatus</code>&nbsp;while a wallet's migration transactions were in the mempool. (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3987" target="_blank">#3987</a>)</li><li>We fixed an issue where the wallet would incorrectly calculate the amount to migrate and would not send as many migration transactions as it could each round of migration. (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3990" target="_blank">#3990</a>)</li><li>We fixed an issue that could cause Zcashd to crash while generating migration transactions if a wallet had a large number of sprout notes. (<a href="https://github.com/zcash/zcash/pull/3990" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3990</a>)</li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 id="mce_15">v2.0.5-2</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>We prevented zcashd from trying to send migration transactions when it is syncing. (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3987" target="_blank">#3987</a>)</li><li>We increased the expiry height for migration transactions to 450. (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3995" target="_blank">#3995</a>)</li><li>We added additional logging to the Sprout to Sapling migration tool. (<a href="https://github.com/zcash/zcash/pull/4002" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#4002</a>)</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><br>For a complete list of changes in 2.0.5, 2.0.5-1 and 2.0.5-2, see the <a href="https://github.com/zcash/zcash/milestone/79?closed=1" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">2.0.5 milestone</a>. </p>
<!-- /wp:paragraph -->