---
ID: 8531
post_title: 'New Release: 2.0.7'
post_name: new-release-2-0-7
post_date: 2019-08-26 15:29:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-7/
published: true
tags:
  - block times
  - Blossom
  - releases
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>In the v2.0.7 release we have implemented&nbsp;<a href="https://github.com/zcash/zips/blob/master/zip-0208.rst">ZIP208</a>&nbsp;which will take effect when Blossom activates. Upon activation, the block times for Zcash will decrease from 150 seconds to 75 seconds, and the block reward will decrease accordingly. This affects at what block height halving events will occur, but should not affect the overall rate at which Zcash is mined. The total founders' reward stays the same, and the total supply of Zcash is decreased only microscopically due to rounding.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This release also includes Blossom activation on testnet, bringing shorter block times. The testnet Blossom activation height is 584000.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Changes needed for the Insight explorer have been incorporated into Zcash as well. <em>This is an experimental feature</em> and therefore is subject to change. To enable, add the <code>experimentalfeatures=1</code>, <code>txindex=1</code>, and <code>insightexplorer=1</code> flags to <code>zcash.conf</code>. This feature adds several RPCs to <code>zcashd</code> which allow the user to run an Insight explorer. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For more details please also go to: <a href="https://z.cash/upgrade/blossom/">https://z.cash/upgrade/blossom/</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1>Summary of the Changes Included in this Release</h1>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Shorter block times.</li><li>Blossom activation on testnet.</li><li>Insight explorer changes.</li></ul>
<!-- /wp:list -->