---
ID: 7374
post_title: The Zcash Reference Wallet Is Here!
post_name: the-zcash-reference-wallet-is-here
post_date: 2019-04-05 15:13:32
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/the-zcash-reference-wallet-is-here/
published: true
tags:
  - Sapling
  - Wallet
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>The light client reference wallet has been built! Sapling shielded transactions now work on mobile devices and we are ready for third-party devs to start providing feedback on the code. What previously required gigabytes of data on a server is now accomplished with megabytes of data and computation suitable for a phone.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To get started, we recommend looking at our <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash-android-wallet-sdk" target="_blank">Android SDK</a>, which interacts with the server (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash-hackworks/lightwalletd" target="_blank">lightwalletd</a>) and light client (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/librustzcash" target="_blank">librustzcash</a>). These resources provide an overview of how all the parts work together<em>—</em> for instance, see what the light client requests from the server, how the received inputs are processed, and how those outputs are used to create transactions. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is the fourth installment in our series about the progress and development of the Zcash reference wallet; we invite you to look back at previous articles about <a href="https://z.cash/blog/introducing-the-zcash-reference-wallet/">our goals and what we’re building</a>, <a href="https://z.cash/blog/zcash-reference-wallet-design/">user experience, interface and styling</a> and <a href="https://z.cash/blog/zcash-reference-wallet-light-client-protocol/">the underlying protocol</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Where to Find the Code </h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Like other Zcash code, it’s open sourced and always will be. </p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash-android-wallet-sdk" target="_blank">Zcash Android SDK: </a>A lightweight SDK that connects Android and Zcash;</li><li><a href="https://github.com/str4d/librustzcash/tree/preview/zcash_client_backend" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Librustzcash</a>: &nbsp;A zcashd for light clients;</li><li><a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash-hackworks/lightwalletd" target="_blank">Lightwalletd</a>: A stateless server that transforms blocks for the light client;</li><li><a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash-android-wallet-poc" target="_blank">Zcash Android reference wallet</a>: An app and resource that incorporate the components.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Our Vision for the Reference Wallet</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We call this wallet a “reference” because it is intended for learning and demonstrative purposes. It is a guide for the ecosystem rather than a competitor within it. At a recent Zcash meetup in San Francisco, a developer was delighted to learn that we actually <em>wanted</em> him to use the reference wallet as a blueprint. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Electric Coin Company is committing to supporting the light client code. We want the Android SDK to be useful for mobile developers. Currently, the reference wallet is only available on Android and compatible with testnet. Some near future plans include improving the documentation and code tests as indicated by the Android SDK disclaimers. <br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If you have questions, head over to the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://chat.zcashcommunity.com/channel/reference-wallet" target="_blank">reference wallet chat channel</a> to talk with the reference wallet team. We encourage and appreciate feedback in the form of PRs, comments, and new issues on any of the code repositories above. Also, we suggest keeping an eye on the <a href="https://github.com/zcash/zips/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">ZIPs repository</a> for proposals which improve the reference wallet or light client code. Like everything we do, community collaboration is critical to the success of this project. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><br>We look forward to continuing to work with the Zcash ecosystem to bring financial freedom to everyone. We believe that the adoption of shielded addresses by services like wallets and exchanges will accelerate us toward that goal. This milestone for the reference wallet is just the beginning—stay tuned for updates by following this blog and <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://twitter.com/electriccoinco" target="_blank">our Twitter account</a>. </p>
<!-- /wp:paragraph -->