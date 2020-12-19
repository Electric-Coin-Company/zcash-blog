---
ID: 7167
post_title: 'New Release: 2.0.4'
post_name: new-release-2-0-4
post_date: 2019-03-27 17:45:26
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-0-4/
published: true
tags:
  - bugs
  - consensus
  - releases
  - Sapling
  - sprout
  - turnstile
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>This release of Zcashd v2.0.4 fixes a Sprout wallet security bug, fixes miner address selection behaviour and introduces a new consensus rule on testnet to reject blocks that violate turnstiles. Zcashd v2.0.4 will be supported until block 569112, expected to arrive around July 15th, 2019, at which point the software will end-of-support halt and shut down.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Notable Changes in this Release</h2>
<!-- /wp:heading -->
<!-- wp:heading {"level":3} -->
<h3>Sprout note validation bug fixed in wallet</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>We include a fix for a bug in the Zcashd wallet which could result in Sprout z-addresses displaying an incorrect balance. Sapling z-addresses are not impacted by this issue.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>This bug would occur if someone sending funds to a Sprout z-address intentionally sent a different amount in the note commitment of a Sprout output than the value provided in the ciphertext (the encrypted message from the sender). A symptom of this bug is the error message "logic error: witness of wrong element for joinsplit input" when attempting to send Sprout funds.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Users should install this update and then rescan the blockchain by invoking <code>zcashd -rescan</code>. Sprout address balances shown by the zcashd wallet should then be correct.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Thank you to Alexis Enston for bringing this to our attention.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><a href="https://z.cash/support/security/announcements/security-announcement-2019-03-19/">Security Announcement 2019-03-19</a></p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>Miner address selection behaviour fixed</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Zcash inherited a bug from upstream Bitcoin Core where both the internal miner and RPC call&nbsp;<code>getblocktemplate</code> would use a fixed transparent address, until RPC <code>getnewaddress</code>&nbsp;was called, instead of using a new transparent address for each mined block. This was fixed in Bitcoin 0.12 and we have now merged the change.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Miners who wish to use the same address for every mined block, should use the&nbsp;<code>-mineraddress</code>&nbsp;option.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><a href="https://zcash.readthedocs.io/en/latest/rtd_pages/zcash_mining_guide.html" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Mining Guide</a></p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>New consensus rule: Reject blocks that violate turnstile (Testnet only)</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Testnet nodes will now enforce a consensus rule which marks blocks as invalid if they would lead to a turnstile violation in the Sprout or Sapling value pools. The motivations and deployment details can be found in the accompanying&nbsp;<a href="https://github.com/zcash/zips/blob/master/zip-0209.rst" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>The consensus rule will be enforced on mainnet in a future release.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Summary of the Changes Included in this Release</h2>
<!-- /wp:heading -->
<!-- wp:list {"ordered":true} -->
<ol><li>Fix Sprout note validation bug in wallet (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3897" target="_blank">#3897</a>)</li><li>Fix default miner address behaviour (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3762" target="_blank">#3762</a>)</li><li>Add consensus rule on testnet to reject blocks that violate turnstile (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3885" target="_blank">#3885</a>)</li><li>Sapling benchmarks updated (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3657" target="_blank">#3657</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3843" target="_blank">#3843</a>)</li><li>Boost, OpenSSL, Rust and Proton dependencies updated (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3809" target="_blank">#3809</a>). AMQP users should review the&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3786#issuecomment-459022118" target="_blank">Proton security fixes</a>.</li><li>Backported 'size_on_disk' field to RPC call 'getblockchaininfo' (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3639" target="_blank">#3639</a>)</li><li>Docs folder updated (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3819" target="_blank">#3819</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3846" target="_blank">#3846</a>)</li><li>Security related documentation updated (<a href="https://github.com/zcash/zcash/pull/3890" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3890</a>,&nbsp;<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3892" target="_blank">#3892</a>)</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>For a more complete list of changes, please see the&nbsp;<a href="https://github.com/zcash/zcash/pulls?q=is%3Apr+milestone%3Av2.0.4+is%3Aclosed" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">2.0.4</a>&nbsp;milestone.</p>
<!-- /wp:paragraph -->