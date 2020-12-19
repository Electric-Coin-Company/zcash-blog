---
ID: 9700
post_title: 'New Release: 3.0.0'
post_name: new-release-3-0-0
post_date: 2020-05-27 22:03:49
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-3-0-0/
published: true
tags:
  - heartwood
  - releases
categories:
  - General
  - Technical
---
<!-- wp:heading {"level":3} -->
<h3>Heartwood activation on mainnet</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release supports the <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/introducing-heartwood/">Heartwood</a> activation on mainnet, which will occur at a block height of 903000 (mid-July), following the targeted EOS halt of our 2.1.2-3 release. Please upgrade to this release, or any subsequent release, in order to follow the Heartwood network upgrade on mainnet.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Heartwood network upgrade deploys <a href="https://zips.z.cash/zip-0213" target="_blank" rel="noreferrer noopener">ZIP 213</a>, which allows miners to <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/mine-to-shielded-coinbase/">mine directly into shielded addresses</a>. It also deploys <a href="https://zips.z.cash/zip-0221" target="_blank" rel="noreferrer noopener">ZIP 221</a>, enabling <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/explaining-flyclient/">Flyclient support</a> by changing the semantics of existing block header fields. The deployment process for the Heartwood upgrade is described in <a href="https://zips.z.cash/zip-0250" target="_blank" rel="noreferrer noopener">ZIP 250</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In order to help the ecosystem prepare for the mainnet activation, Heartwood has <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-1-2-3/">already been activated</a> on the Zcash testnet. Any node version 2.1.2 or higher, including this release, supports Heartwood on testnet as well.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":25} -->
<div style="height:25px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Mining to Sapling shielded addresses</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>After the mainnet activation of Heartwood, miners will be able to mine directly into a Sapling shielded address. Miners should wait until after Heartwood activation before they make changes to their configuration to leverage this new feature.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>After activation of Heartwood, miners can add <code>mineraddress=SAPLING_ADDRESS</code> to their <code>zcash.conf</code> file, where <code>SAPLING_ADDRESS</code> represents a Sapling address that can be generated locally with the <code>z_getnewaddress</code> RPC command. Restart your node, and block templates produced by the <code>getblocktemplate</code> RPC command will now have coinbase transactions that mine directly into this shielded address.</p>
<!-- /wp:paragraph -->