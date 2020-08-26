---
ID: 7560
post_title: Sprout-to-Sapling Migration Tool
post_name: sprout-to-sapling-migration-tool
post_date: 2019-05-21 11:07:57
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/sprout-to-sapling-migration-tool/
published: true
tags:
  - explainers
  - migration tool
  - privacy
  - Sapling
  - shielded addresses
  - sprout
  - transactions
  - turnstile
categories:
  - General
  - Privacy
  - Technical
---
<!-- wp:paragraph -->
<p>The Electric Coin Company is pleased to announce the official Sprout-to-Sapling migration tool in the <a href="/blog/new-release-2-0-5-2/">2.0.5-2 release</a> of zcashd. This tool comes in the form of new RPCs with the purpose of automatically and safely migrating the funds in Sprout addresses to Sapling addresses. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Only users with funds in Sprout addresses need to use this tool. Users can confirm if they have funds in a Sprout address by checking to see if any of their addresses start with a “zc”. Sapling addresses are the standard shielded address since the Sapling network upgrade and start with a “zs”.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Why it’s needed</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The privacy properties of shielded addresses (both Sprout and Sapling) make direct auditing of the total monetary supply impossible. Therefore, a <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html#turnstiles" target="_blank">turnstile</a> mechanism is implemented to monitor value entering and exiting their associated <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html#value-pools" target="_blank">value pools</a>. The turnstile prohibits direct transfer between shielded value pools without revealing the amount being moved. While this mechanism enhances auditing capabilities, revealing balances introduces <a href="/blog/maintaining-privacy/">privacy concerns</a>. The Sprout-to-Sapling migration tool automates the process of moving funds to Sapling addresses in a way that reduces the potential for compromising user privacy. </p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>How it works</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This migration tool hides individual migration transactions among those of all users who are doing the migration at around the same time. Whenever the blockchain reaches a 500 block height interval, up to 5 migration transactions are created with transaction amounts picked according to a random distribution. The full specification of this tool can be found in <a href="https://github.com/zcash/zips/blob/master/zip-0308.rst" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP 308</a>.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To migrate funds, zcashd users simply enable or disable the tool with z_setmigration. To check the status of the migration, users can call z_getmigrationstatus. Documentation for using these RPCs can be accessed in the official <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html#migration-tool" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">migration tool docs</a>. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The migration tool is supported in zcashd v2.0.5-2 and up; for the latest version see the <a href="https://z.cash/download">download</a> page. We recommend third-party wallets that support both Sprout and Sapling addresses implement this tool as well. </p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Further Motivation</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Before the activation of the Sapling Network Upgrade, we <a href="/blog/sapling-addresses-turnstile-migration/">wrote</a> about the benefits of Sapling addresses and the risks associated with fund migration from legacy Sprout addresses. We supplied guidelines for manual migration in lieu of not having the tool ready but no longer recommend for anyone to migrate manually. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The release of this tool is timed with the introduction of new consensus code which uses the turnstiles to enforce <a href="/blog/turnstile-enforcement-against-counterfeiting/">defense against counterfeiting</a>. We hope that everyone who has ZEC in Sprout addresses will make use of this tool to safely move their funds. We look forward to increasing adoption of Sapling addresses across the Zcash ecosystem. Please connect with us in the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://chat.zcashcommunity.com" target="_blank">community chat</a> or <a href="https://forum.zcashcommunity.com" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">community forum</a> if you have any questions. <br></p>
<!-- /wp:paragraph -->