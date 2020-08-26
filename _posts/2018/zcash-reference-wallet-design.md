---
ID: 5715
post_title: Zcash Reference Wallet Design
post_name: zcash-reference-wallet-design
post_date: 2018-11-26 10:33:34
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/zcash-reference-wallet-design/
published: true
tags:
  - Wallet
categories:
  - General
---
<!-- wp:paragraph -->
<p>A reference implementation is concrete and functioning code that proves that a concept can work. Our reference wallet aims to prove that Zcash shielded transactions can work on mobile devices with limited resources, now that the <a href="https://z.cash/upgrade/sapling/">Sapling network upgrade</a> is live. From the <a href="https://z.cash/blog/introducing-the-zcash-reference-wallet/">last design post</a>, we know the main goal of the reference wallet is to increase adoption of Zcash and promote the use of shielded addresses. This blog post digs deeper into our UX considerations and provides an overview of our design decisions and rationale.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"align":"center","width":1200,"height":501} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="/wp-content/uploads/2018/11/blog-Zcash-Reference-Wallet-Design-01.png" alt="Zcash Proof of Concept Light Wallet: Onboarding - Create &amp; Restore + Tutorial design examples" width="1200" height="501"/><figcaption>The onboarding flow has been simplified to reduce barrier to entry, and also forces users to prove they have saved their seed phrase.</figcaption></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>Our hope is to create a standard of UX patterns for other Zcash wallets to use in their implementations for consistency. We aim to reduce friction for using Zcash and create faster and smoother transactions, while allowing more users to understand the underlying technology. We also want to help the entire cryptosphere solve the common problems that all wallets have to deal with.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Currently, there are a number of ways to use Zcash, but the most heavy use is carried out by exchanges, traders, and individuals running their own nodes or mining rigs. Software and hardware wallets do exist, but the feasibility of shielded mobile ones has only become possible with the <a href="https://z.cash/upgrade/sapling/">activation of Sapling</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We wanted to ensure the best user experience, with the best usability. To that end, we decided to follow <a href="https://material.io/design/" target="_blank" rel="noreferrer noopener">Google’s Material Design library</a> and only deviate when we had clear reasoning. This way we build on top of well-researched design decisions and styling for common elements such as buttons, menus, and modals and focus on designing to communicate various states of a cryptocurrency transaction, visualizing addresses and backup seeds, and other novel concepts. This ensures the conversation is about features and functionality, not new design decisions.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"align":"center","width":1200,"height":452} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="/wp-content/uploads/2018/11/blog-Zcash-Reference-Wallet-Design-02.png" alt="Zcash Proof of Concept Light Wallet: General Use - Balance, Send, Receive and Request screen designs" width="1200" height="452"/><figcaption>The first version of the reference wallet allows users to send, receive, and request Zcash at a sapling Zcash address.</figcaption></figure></div>
<!-- /wp:image -->
<!-- wp:heading -->
<h2>Design Methodology</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Let's take a moment to talk about our design methodology. It is quite simple and dictates a certain workflow:</p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol><li><strong>Stay grounded. </strong>We use personas to create use-cases for real users.</li><li><strong>Rapid prototype</strong> and <strong>iterate often</strong> based on testing.</li><li><strong>Test early and often. </strong>We use both qualitative and quantitative research methods to analyze the problem space and design better solutions.</li><li><strong>Listen to our users.</strong> We are creating a feedback program allowing users to open conversations, comment anonymously, or generally get in touch with us about their experiences. Additionally, we use this information to help redefine our personas.</li><li><strong>Grow. </strong>We will continue to watch, learn, and enhance features.</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>User Experience Considerations</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>So now that we know what and who we are designing for, we can talk about user experience. There are a number of User Experience considerations we want to keep in mind as we design our application. Here they are, ranked by priority:</p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol><li><strong>Preventing loss of funds</strong> - While trying to create an easier onboarding experience, a few wallets have made it easier for users to accidentally skip backing up their seed phrases (and therefore their wallets). This can often end in losing access to funds forever, so we have worked hard to make sure they have correctly written down their seed phrase.</li><li><strong>Reduce learning curve and barrier to entry</strong> - Most wallets expect expert users, and often don’t take advantage of the teaching moments available through a normal onboarding. We’ve created an onboarding that is not only easier but also helps ensure the user understands the steps taken to protect their privacy. Additionally, we maintain usability and accessibility (font sizes, using colors and symbols to denote states, etc).</li><li><strong>Zcash-specific features</strong> - Our wallet has a few unique features we have emphasised within the application. All transactions are shielded by default and include a shield icon inside the transaction details. Also, while sending, you may add an encrypted memo for your recipient.</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>The following video includes a run-through of receiving, sending, and requesting ZEC with our reference wallet. Take a look and <a href="mailto:design@z.cash">let us know what you think!</a></p>
<!-- /wp:paragraph -->
<!-- wp:core-embed/youtube {"url":"https://youtu.be/m9V55KKxpQs","type":"video","providerNameSlug":"youtube","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
https://youtu.be/m9V55KKxpQs
</div><figcaption>A design prototype of the reference wallet that previews how we want our application to function after set up.</figcaption></figure>
<!-- /wp:core-embed/youtube -->
<!-- wp:heading -->
<h2>Coming up</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>A series of blog posts will feature specific areas of the reference wallet work:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>Protocol: technical challenges, interacting components, and privacy goals</li><li>Implementation: target devices, build methodology, and security measures</li><li>Results: early feedback, user testing, and what we have learned</li></ul>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>Come back to <a href="https://z.cash/blog/">the Zcash blog</a> or follow us on <a href="https://twitter.com/electriccoinco">Twitter</a> for further updates!</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->