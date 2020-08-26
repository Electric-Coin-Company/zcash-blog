---
ID: 9850
post_title: >
  7 things we learned building the
  shielded-first ECC Wallet
post_name: >
  7-things-we-learned-building-the-shielded-first-ecc-wallet
post_date: 2020-06-11 23:34:49
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/7-things-we-learned-building-the-shielded-first-ecc-wallet/
published: true
tags:
  - developer
  - wallets
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Earlier this year, ECC released <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/ecc-releases-resources-for-building-mobile-shielded-zcash-wallets/">a suite of libraries for building shielded mobile wallets</a> in support of the shielded-Zcash ecosystem. We used these wallet libraries to build ECC Wallet, a fully-functional, shielded-first app for sending, receiving and storing Zcash. Yesterday — to support continued community-driven development and ahead of the <a rel="noreferrer noopener" href="https://gitcoin.co/hackathon/privacy/onboard" target="_blank">Protect Privacy hackathon</a> — we released the source code for both Android and iOS.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We learned a lot in the process of building and designing the ECC Wallet. This exercise helped us understand first-hand the joys and challenges developer teams experience when building privacy-preserving tools and services. We'll touch on some of those lessons learned below, but if you are interested in learning more, don’t hesitate to <a rel="noreferrer noopener" href="https://discord.gg/PgcDjbm" target="_blank">get in touch</a>.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":24} -->
<div style="height:24px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Lessons from the wallet team</h3>
<!-- /wp:heading -->

<!-- wp:media-text {"mediaId":9892,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9892","mediaType":"image","mediaWidth":15,"className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Kevin_circ-1.png" alt="" class="wp-image-9892"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Kevin</strong> <strong>(Android engineer):&nbsp;</strong>"Privacy is harder than security. And, in fact, privacy requires security! And like security, if you don’t factor that in the beginning, it’s impossible to accidentally create a system that is private. There is also a tricky tradeoff between functionality and privacy."</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9890,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9890","mediaType":"image","mediaWidth":15,"verticalAlignment":"top","className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile is-vertically-aligned-top in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Pacu_circ-1.png" alt="" class="wp-image-9890"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Pacu (iOS engineer):</strong> "I learned the beautiful value of test-driven development. When you have a component to build, and it’s doing something completely new, you are able to work on small features, one at a time. With 10 years experience as an iOS developer, building from scratch is such a fun and rare privilege. It’s not as exciting when you get into a huge codebase with lots of existing code."</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9888,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9888","mediaType":"image","mediaWidth":15,"verticalAlignment":"top","className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile is-vertically-aligned-top in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Larry-circ-1.png" alt="" class="wp-image-9888"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Larry (software engineer):</strong> "I learned a lot about Golang, the language that lightwalletd is implemented in. Specifically, I had a great time with the test framework, which is built into the language. In other languages, it is a separate add-on package (zcashd has two unit test frameworks). The Go test framework integrated very nicely, and the Go debugger, <a rel="noreferrer noopener" href="https://github.com/go-delve/delve" target="_blank">delve</a>, is also awesome. <a rel="noreferrer noopener" href="https://github.com/fullstorydev/grpcurl" target="_blank">grpcurl</a>, the gRPC command-line tool, has been super helpful in sending requests into lightwalletd (as if from a mobile wallet)."</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9881,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9881","mediaType":"image","mediaWidth":15,"verticalAlignment":"top","className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile is-vertically-aligned-top in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Geffen-circ-1.png" alt="" class="wp-image-9881"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Geffen</strong> <strong>(design lead):&nbsp;</strong>"There is a tension between user needs and protocol limitations. For instance, people want assurance that their money has been sent safely faster than a block can be confirmed or to cancel transactions before expiry. We’ve created a UX that addresses these needs by giving users the right information and allowing on-device cancellation before transactions are submitted to the network."&nbsp;</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9879,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9879","mediaType":"image","mediaWidth":15,"verticalAlignment":"top","className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile is-vertically-aligned-top in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Taylor-circ-1.png" alt="" class="wp-image-9879"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Taylor</strong> <strong>(information security engineer):&nbsp;</strong>"I learned a new, user-centric way to threat model. A normal threat model is a list of attacks, but we inverted it and started out with the security and privacy guarantees that users care about. Then we worked backwards from that to see what we needed to do. The normal threat model process is to try to brainstorm all the things that could go wrong and all the types of attacks; it’s easy to miss things, because no one can get all the things that can go wrong. This new approach scoped the conversation appropriately for our needs."&nbsp;</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9873,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9873","mediaType":"image","mediaWidth":15,"verticalAlignment":"top","className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile is-vertically-aligned-top in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Brad-circ-1.png" alt="" class="wp-image-9873"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph -->
<p><strong>Brad (senior product manager and engineering manager):</strong>&nbsp;"It’s difficult to manage all of the various dependencies — since we’re doing this on two different mobile platforms and five different languages — between zcashd, librustzcash, lightwalletd, Android SDK and iOS SDK. We combatted this by utilizing the similarities as much as possible. For instance, the APIs for Android and iOS are designed intentionally to be nearly functionally identical so that we did not need a unique architecture for each."</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":57} -->
<div style="height:57px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:media-text {"mediaId":9886,"mediaLink":"https://dev-electriccoinco-wordpress.pantheonsite.io/?attachment_id=9886","mediaType":"image","mediaWidth":15,"className":"in-blog-thumb"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile in-blog-thumb" style="grid-template-columns:15% auto"><figure class="wp-block-media-text__media"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Linda-circ-1.png" alt="" class="wp-image-9886"/></figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…","fontSize":"normal"} -->
<p class="has-normal-font-size"><strong>Linda (product manager): </strong>"ECC values community-driven development and keeping our code open-sourced over any risks associated with making the code public. The possibility that someone else might make a better app than we did is not a risk to us, but a reward."&nbsp;</p>
<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:spacer {"height":28} -->
<div style="height:28px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:spacer {"height":28} -->
<div style="height:28px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3><strong>Supporting community-driven development</strong></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/dev-fund-poll-shows-consensus/" target="_blank" rel="noreferrer noopener">Zcash Major Grants</a> will soon open up ecosystem funding for independent developers. ECC is committed to cultivating a thriving community of wallet developers. Don’t wait to get started. Check out our developer resources and <a href="https://discord.gg/PgcDjbm" target="_blank" rel="noreferrer noopener">get in touch with the wallet team</a>.</p>
<!-- /wp:paragraph -->