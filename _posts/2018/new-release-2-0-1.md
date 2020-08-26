---
ID: 5430
post_title: 'New Release: 2.0.1'
post_name: new-release-2-0-1
post_date: 2018-10-15 11:45:58
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-0-1/
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
<p>This release introduces Sapling support into the wallet RPC of the Zcash node software!</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":1} -->
<h1>Sapling Activation</h1>
<!-- /wp:heading -->
<!-- wp:heading -->
<h2>Mainnet</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>This release is consensus-compatible with the Sapling network upgrade and adds significant support in the zcashd wallet RPC. We’re encouraging all users and miners to upgrade as soon as possible. The first block of Sapling will be block 419200, which is expected to be mined on the 28th of October 2018, the second anniversary of Zcash’s official launch. More information on the upcoming Sapling network upgrade can be found below:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li><a href="https://z.cash/upgrade/sapling.html">Sapling Network Upgrade</a></li><li><a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html">Sapling Turnstile</a></li><li><a href="https://zcash.readthedocs.io/en/latest/rtd_pages/nu_dev_guide.html">Network Upgrade Dev Guide</a></li></ul>
<!-- /wp:list -->
<!-- wp:heading -->
<h2>Testnet</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Sapling has activated on the testnet at block 280000. If you are running a v2.0.1 node, you no longer need to specify&nbsp;<code>-experimentalfeatures</code>&nbsp;and&nbsp;<code>-developersapling</code>&nbsp;to use Sapling functionality on testnet. If you are running an older v2.0.0 node, please upgrade to version v2.0.1 which introduced a consensus rule change to allow min difficulty blocks to be mined from block 299188, thereby splitting the chain.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":1} -->
<h1>Other Notable Changes</h1>
<!-- /wp:heading -->
<!-- wp:heading -->
<h2>Sapling RPC Support</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>This release contains support for Sapling RPC functionality on mainnet, enabling the sending and receiving of Sapling shielded funds.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Hierarchical Deterministic Key Generation</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>All Sapling addresses will use hierarchical deterministic key generation according to <a href="https://github.com/zcash/zips/blob/master/zip-0032.rst">ZIP 32</a> (<code>keypath m/32'/133'/k'</code>&nbsp;on mainnet). Transparent and Sprout addresses will still use traditional key generation.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Master seeds of HD wallets, regardless of when they have been created, can be used to re-generate all possible Sapling private keys. <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/wallet_backup.html">Regular backups</a> are still necessary, however, in order to ensure that transparent and Sprout addresses are not lost.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>A future release will support the importing and restoration of HD wallets.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Fix Signing Raw Transactions with Unsynced Offline Nodes</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>In&nbsp;<code>signrawtransaction</code>&nbsp;we determine the consensus branch ID (which we then later use to construct the transaction) using the chain height. We now also consider the&nbsp;<code>APPROX_RELEASE_HEIGHT</code>&nbsp;, as this is a better estimation than 0 for the height of the chain if we are unsynced. We have also added an additional parameter to&nbsp;<code>signrawtransaction</code>&nbsp;to allow manually overriding the consensus branch ID that zcashd determines we are on.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":1} -->
<h1>Summary of the Changes Included in this Release</h1>
<!-- /wp:heading -->
<!-- wp:list {"ordered":true} -->
<ol><li>Allow minimum-difficulty blocks on testnet (<a href="https://github.com/zcash/zcash/pull/3559">#3559</a>)</li><li>Enable Sapling features on mainnet (<a href="https://github.com/zcash/zcash/pull/3537">#3537</a>)</li><li>Use ZIP 32 for all Sapling spending keys (<a href="https://github.com/zcash/zcash/pull/3492">#3492</a>)</li><li>Fix signing raw transaction with unsynced offline node (<a href="https://github.com/zcash/zcash/pull/3520">#3520</a>)</li><li>Sapling support for persisting wallet to disk (<a href="https://github.com/zcash/zcash/pull/3517">#3517</a>)</li><li>Add Sapling RPC support to z_shieldcoinbase (<a href="https://github.com/zcash/zcash/pull/3518">#3518</a>)</li><li>Add Sapling RPC support to z_listunspent (<a href="https://github.com/zcash/zcash/pull/3510">#3510</a>)</li><li>Add Sapling RPC support to z_listreceivedbyaddress (<a href="https://github.com/zcash/zcash/pull/3499">#3499</a>)</li><li>Add Sapling RPC support to z_importwallet and z_exportwallet (<a href="https://github.com/zcash/zcash/pull/3491">#3491</a>)</li><li>Add Sapling RPC support to z_sendmany (<a href="https://github.com/zcash/zcash/pull/3489">#3489</a>)</li><li>Add Sapling RPC support to z_getbalance and z_gettotalbalance (<a href="https://github.com/zcash/zcash/pull/3436">#3436</a>)</li><li>Track Sapling notes and nullifiers in the wallet (in-memory only, no persistence to disk) (<a href="https://github.com/zcash/zcash/pull/3422">#3422</a>)</li><li>Make NU peer management logic upgrade-agnostic (<a href="https://github.com/zcash/zcash/pull/3512">#3512</a>)</li><li>Generate an ovk to encrypt outCiphertext for Sapling t-addr senders (<a href="https://github.com/zcash/zcash/pull/3516">#3516</a>)</li><li>Windows cross-compile support (<a href="https://github.com/zcash/zcash/pull/3172">#3172</a>)</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>To view a complete list of changes, please see the&nbsp;<a href="https://github.com/zcash/zcash/pulls?q=is%3Apr+is%3Aclosed+milestone%3Av2.0.1">2.0.1</a>&nbsp;milestone.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For information on specific Sapling RPC parameter changes, please see the Network Upgrade Developer guide on&nbsp;<a href="https://zcash.readthedocs.io/en/latest/rtd_pages/nu_dev_guide.html#using-zcashd-unmodified">using zcashd unmodified.</a></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->