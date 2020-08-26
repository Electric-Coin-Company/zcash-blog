---
ID: 9400
post_title: Introducing Heartwood
post_name: introducing-heartwood
post_date: 2020-03-25 16:03:36
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/introducing-heartwood/
published: true
tags:
  - network upgrade
categories:
  - General
---
<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>Heartwood, the next major Zcash network upgrade, improves interoperability through Flyclient support and gives miners the option to immediately shield mining rewards in coinbase transactions. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The community chose the name “Heartwood” to evoke themes of faster growth, adoption and expansion. The two ZIPs in Heartwood are ZIP 221 (FlyClient) and ZIP 213 (Shielded Coinbase). The block height for Heartwood will be announced in Q2.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":36} -->
<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>ZIP 221: Flyclient</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Flyclient enables interoperability efforts, cross-chain integration and light-client use cases. This ZIP has the potential to enable multiple interoperability protocols and products or services built upon them. This is particularly exciting as we look ahead to November, when Zcash Major Grants will open up funding for more developers to work on top of Zcash.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This ZIP specifies modifications to be made to the Zcash block header format to include Merkle Mountain Range (MMR) commitments. These commitments allow efficient proofs of Proof-of-Work for light clients, enabling future adoption of the FlyClient protocol. This could allow Zcash SPV proofs to be verified in blockchains such as Ethereum, enabling efficient cross-chain communication and pegs. It also reduces bandwidth and storage requirements for resource-limited clients like mobile or IoT devices.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For the full text of this ZIP, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zips.z.cash/zip-0221" target="_blank">click here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":36} -->
<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>ZIP 213: Shielded Coinbase</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A coinbase transaction is a unique type of transaction that is created by a miner and includes the rewards for a mined block. Until Heartwood, Zcash miners were only able to send mining rewards to a transparent address. This ZIP defines modifications to the Zcash consensus rules that enable coinbase funds to be mined to shielded Sapling addresses.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Prior to the Sapling upgrade, a shielded coinbase was not feasible because shielded transactions required significant memory and CPU resources to create. The Sapling network upgrade deployed architectural changes and performance improvements that make shielding funds directly in the coinbase transaction possible. The ZIP does not require that all coinbase must be shielded. This is so that miners and mining pools will have the option of using either transparent addresses or Sapling addresses.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Shielded coinbase is an important milestone for Zcash network privacy and the overall size of the anonymity set. We anticipate that ZIP 213 will drive more demand for shielded support across the ecosystem.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For the full text of this ZIP, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zips.z.cash/zip-0213" target="_blank">click here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>The <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://forum.zcashcommunity.com/t/ecc-s-nu3-feature-selection/33832" target="_blank">feature selection</a> was determined in the community forum in June 2019. Since then, the Electric Coin Co. has completed <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/security-assessments-nu3-specifications-blossom-implementation-and-sapling-documentation/">security assessments</a> on Heartwood specifications and worked with the Zcash Foundation and other parties to ensure consensus ahead of this network upgrade.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For the past four years, ECC has established a reputation of shipping quality, production-ready code. We are proud of our regular and reliable release schedule, having already begun work on NU4. Heartwood is a mandatory network upgrade designed to improve interoperability and privacy. If you are a miner or network node, please stay tuned for more information regarding the Heartwood activation date. If you have any questions, <a href="https://discord.gg/PgcDjbm" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">reach out to us</a>.<br></p>
<!-- /wp:paragraph -->