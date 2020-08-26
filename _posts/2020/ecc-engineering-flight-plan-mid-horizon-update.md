---
ID: 9342
post_title: 'ECC Engineering flight plan: Mid-horizon update'
post_name: >
  ecc-engineering-flight-plan-mid-horizon-update
post_date: 2020-03-03 21:54:45
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/ecc-engineering-flight-plan-mid-horizon-update/
published: true
tags:
  - Flight Plan
  - protocol
  - roadmap
categories:
  - General
  - Technical
---
<!-- wp:spacer {"height":34} -->
<div style="height:34px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>In our <a href="https://www.youtube.com/watch?v=yYFh0CCye58" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">2019 Q4 livestream</a>, we mapped out our Engineering flight plan aimed at advancing the future of Zcash across a multi-year timeframe. In that presentation, we defined three time horizons and our product plans associated with each: a 0-to-6-month period, a 6-to-24-month period and a 24-to-48-month period.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":9362,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/03/Flightplan1-800x450.png" alt="" class="wp-image-9362"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>This post provides a mid-horizon update to that flight plan and provides insights into our Engineering activities for Q1 2020 that align with the goals presented there. We also provided a similar update in our <a href="https://www.youtube.com/watch?v=HX2AZcHZHBo" target="_blank" rel="noreferrer noopener" aria-label="most current livestream (opens in a new tab)">most current livestream</a>. Like any product plan, the further out the planning periods go in these horizons, the less well-defined the plans are and the more likely they are to change. And while we talk about horizons as far as four years out, the <em>activities</em> described here are just those for the current quarter.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":44} -->
<div style="height:44px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Horizon 1</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Horizon 1 is focused on community enablement and interoperability, and we have several activities, both ongoing and planned, for this quarter in support of these goals.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":9364,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/03/Flightplan2-800x450.png" alt="" class="wp-image-9364"/></figure>
<!-- /wp:image -->

<!-- wp:image {"id":9365,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/03/Flightplan3-800x450.png" alt="" class="wp-image-9365"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Flyclient support</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Flyclient support does a couple of things, primarily:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>It enables low-power devices (for example, mobile phones) to send and verify transactions.</li><li>It facilitates cross-chain interoperability protocols.&nbsp;</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Our activities this quarter in support of this goal include the implementation of <a href="https://github.com/zcash/zips/blob/b6be3770c9cbd340b57d6dd6786d43ddf0610189/zip-0221.rst" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP-221</a> and an external implementation audit.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Shielded coinbase implementation</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A coinbase transaction is the first transaction in a block and contains the block reward for the miner. Currently in Zcash, coinbase transactions can only contain transparent outputs, meaning the block rewards can only go to transparent addresses. Shielded coinbase eliminates that requirement and incentivizes miners to shield directly into the Sapling pool.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Our activities for this quarter include the implementation of <a href="https://zips.z.cash/zip-0213" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP-213</a> and conducting an external implementation audit.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It’s worth noting that for any feature (like flyclient and shielded coinbase) that contains consensus changes, we conduct two types of audits: specification and implementation. The specification audits for both of these features have already been done and are available <a href="https://github.com/trailofbits/publications/blob/master/reviews/Zcash.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">here</a> and <a href="https://research.nccgroup.com/wp-content/uploads/2020/02/NCC_Group_Zcash_NU3_Blossom_Report_2020-02-06_v1.1.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">here</a>. <a href="https://www.trailofbits.com/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Trail of Bits</a> also produced an informative Zcash whitepaper that can be found <a href="https://github.com/trailofbits/publications/blob/master/reviews/ZcashWP.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Viewing key RPC support</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Viewing keys allow users to selectively disclose transaction information to third parties. There are multiple use cases for this feature but two of the main ones are regulatory and audit compliance:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Exchanges need to be able to detect deposits into shielded deposit addresses while storing spending authority keys on secure hardware.</li><li>Exchanges and/or custodians need to be able to provide visibility of their shielded Zcash holdings to auditors.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Viewing key support was first deployed into Zcash with the <a href="https://z.cash/upgrade/sapling/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Sapling</a> network upgrade (NU1).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Activities this quarter include making those viewing keys usable by Zcashd.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Testnet-in-a-Box</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Our Testnet-in-a-Box is an incredibly important initiative that allows protocol development teams to spin up a working, multinode testnet then invite others to join and participate in extended testing (assuming consensus compatibility).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This quarter, we’ll be delivering this feature along with a branch running Transparent Zcash Extensions.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Transparent Zcash extensions</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Transparent Zcash Extensions (TZEs) were formerly called Whitelisted Transparent Programs. They’re intended to simplify <a href="https://boltlabs.tech/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">BOLT</a> layer-2 support and extensibility of the consensus rules for other use cases, such as atomic swaps with other blockchains.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Activities planned for this quarter include delivering a prototype implementation of <a href="https://github.com/zcash/zips/blob/575c56593a14eefc698e9e450278eac8969c8848/zip-0222.rst" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIP-222</a> and a TZE branch that can be used with our Testnet-in-a-Box initiative.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Shielded wallet SDKs for iOS and Android</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We’re also doing quite a bit of work this quarter on our shielded wallet SDKs for iOS and Android. As we mentioned in the last livestream, we’re developing an internal-use wallet for both operating systems and learning a lot about wallet UX in the process. We’re currently alpha testing these wallets internally and excited to be open sourcing both the Android and iOS wallets before the end of Q2.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Activities this quarter included continued improvements to the wallet SDKs, continued development and internal rollout of our Android and iOS wallets, and the deployment of a wallet developer information portal.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":51} -->
<div style="height:51px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Horizon 2</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Horizon 2 covers the the 6-to-24-month timeframe — which will take place under a new governance structure, decided by the community in recent dev-fund-related conversations and polling.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":9366,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/03/Flightplan4-800x450.png" alt="" class="wp-image-9366"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Translate development fund decision</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The Zcash community recently voted to create a new dev fund with 20 percent of the mining rewards. The distribution will be as follows: 7% to ECC, 5% to the Zcash Foundation and 8% to support major grant initiatives. More detail on the process and results can be found <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/dev-fund-poll-shows-consensus/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Our primary activity for this quarter is to fulfill the community governance decision by translating this decision into consensus rules we can implement in NU4.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Scalability 2021</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Scalability 2021 is a long-term initiative to transition to a new architecture with layer 1, horizontal scalability. The current focus of this effort is in research and development around Halo, a new proof system that supports recursive proofs without a toxic waste systemic vulnerability.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Our primary activity this quarter includes continued HALO-related R&amp;D, peer review and high-performance implementation work.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Community-driven development</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The next goal is to begin the transition to a community-driven development model, which begins in earnest with the advent of major grants post NU4.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Activity this quarter includes reaching out to protocol development teams involved in NU3 and NU4 to begin to craft a new network upgrade process. We’re incredibly excited about the potential this brings to the Zcash ecosystem and look forward to working with everyone to move Zcash forward.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":61} -->
<div style="height:61px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Horizon 3</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Horizon 3 covers the the 2-to-4-year timeframe, with a focus on layer-1 scalability and a closed loop with regard to the shielded lifecycle.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":9368,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/03/Flightplan5-800x450.png" alt="" class="wp-image-9368"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Scalability 2021 deployment</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The first goal is the deployment of our Scalability 2021 initiative. Ideally, engineering teams should always address scalability before it becomes a concern. In complicated systems and networks, the intricacies of scalability are often complex and there is no quick fix. By beginning work on this long-term initiative now, we ensure we’re ready to deploy well ahead of demand. We want Zcash users to feel confident in their decision to use it, both at a consumer and business level.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Our primary activity this quarter is our continued work on Halo.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Goal: Extending privacy across various bridging protocols</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The next activity is focused on extending privacy across various bridging protocols, creating a privacy network effect. This makes Zcash more valuable to DeFi applications and other blockchains, and it enables use cases such as shielded BOLT channel management.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Activity for Q1 2020 includes early R&amp;D for Shielded Zcash Extensions (SZEs).</p>
<!-- /wp:paragraph -->