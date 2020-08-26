---
ID: 7147
post_title: >
  Turnstile Enforcement Against
  Counterfeiting
post_name: >
  turnstile-enforcement-against-counterfeiting
post_date: 2019-03-22 15:46:01
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/turnstile-enforcement-against-counterfeiting/
published: true
tags:
  - counterfeiting
  - explainers
  - migration tool
  - monetary supply
  - Sapling
  - shielded addresses
  - sprout
  - turnstile
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>The Electric Coin Company has developed consensus code that preserves the Zcash monetary base in the event of a counterfeiting compromise within Zcash’s shielded supply. We intend to deploy this as a backwards compatible consensus rule in the Zcashd v2.0.5 release, <a href="https://z.cash/support/schedule/">scheduled</a> for the beginning of May. We believe this new rule does not materially affect users and is low-risk to deploy.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We are aware of only one previous vulnerability, <a href="https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/">CVE 2019-7167</a>, which before the Sapling network upgrade activation, could have allowed a counterfeiting compromise. Although a compromise was possible, we do not believe that counterfeiting has occurred. The <a href="https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/#summary">full disclosure summary</a> includes a list of those reasons.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Tracking Shielded Value Pools</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>In Zcash, all ZEC resides within “value pools” determined by the type of address holding the ZEC. There are currently three value pools: the <em>transparent value pool</em>, the <em>Sprout value pool</em>, and the <em>Sapling value pool</em>. Because Zcash’s Sprout and Sapling shielded addresses are designed with strong privacy protections, a counterfeiting compromise cannot be directly detected in either of those value pools.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>However, by design, ZEC may only enter or exit shielded value pools by transparently revealing the value of the transfer. This is called the “turnstile.” See the documentation on <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html#value-pools">value pools, turnstiles</a> and the <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html">Sprout to Sapling migration</a> for more details. If a counterfeiting compromise generated illegitimate ZEC within a shielded value pool and more ZEC exited the pool than entered, then the <a href="https://zcha.in/statistics/network">publicly tracked value pool total</a> would become negative. </p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Codifying the Electric Coin Company’s Existing Policy</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Starting in Zcash v2.0.4 <em>on testnet only</em>, and then planned for Zcash v2.0.5 on mainnet, we have developed a consensus change that codifies our published <a href="https://z.cash/blog/defense-against-counterfeiting-in-shielded-pools/">Defense Against Counterfeiting in Shielded Pools</a> policy. The specification in <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/blob/master/zip-0209.rst" target="_blank">ZIP 209</a> is intentionally simple for clarity and broad understanding.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>If the "Sprout value pool balance" or "Sapling value pool balance" would become negative in the block chain created as a result of accepting a block, then all nodes MUST reject the block as invalid.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>An immediate implication is that if a user has funds in a shielded value pool, but the publicly tracked pool balance is less than the user’s funds, they will not be able to transfer all of their funds out of that value pool. This design decision contains counterfeiting bugs inside the affected shielded value pool. Users should be aware of and consider possible ramifications.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>In addition to deployment on testnet in 2.0.4, we will complete parallel simulation tests for the consensus rule before going live on mainnet. The plan is to have both this consensus rule and the Sprout to Sapling migration tool released on mainnet in Zcashd v2.0.5. The purpose of the <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html#migration-tool">migration tool</a> is to protect users’ privacy via automation, avoiding possible human error while doing a manual transfer of funds from Sprout addresses to Sapling addresses. If any changes to this schedule are necessary, we will communicate them through our usual channels. Stay up-to-date with the latest through this blog, the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://forum.zcashcommunity.com/" target="_blank">community forums</a>, the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://chat.zcashcommunity.com/" target="_blank">community chat</a> and <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://twitter.com/electriccoinco" target="_blank">Twitter</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><em>Post update 27 March 2019: ZIP 209 link and context updated to reflect finalized specification.</em></p>
<!-- /wp:paragraph -->