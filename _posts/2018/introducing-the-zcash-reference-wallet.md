---
ID: 5563
post_title: Introducing the Zcash Reference Wallet
post_name: introducing-the-zcash-reference-wallet
post_date: 2018-10-31 12:20:35
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/introducing-the-zcash-reference-wallet/
published: true
tags:
  - Wallet
categories:
  - General
---
<!-- wp:paragraph -->
<p>Our current goal at Zcash Company is to increase the adoption and use of shielded addresses. This work is aimed at empowering everyone with economic freedom and opportunity through an open, permissionless and private payment system.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Zcash Company is building a reference light client wallet featuring a Sapling shielded address that can receive and send transactions. The objective of this project is to prove that shielded transactions can work on mobile devices <em>and</em> to build reusable solutions for functionality required to support shielded addresses. &nbsp;</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Shielded transactions</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Unlike other cryptocurrencies, Zcash has two types of addresses, transparent and shielded. This results in four basic <a href="https://z.cash/blog/anatomy-of-zcash/">types of transactions</a>: transparent, shielding, deshielding and shielded. &nbsp;Shielded transactions, transactions from one shielded address to another, provide the most financial privacy by encrypting identifying data on the blockchain <em>— </em>such as the sender, recipient and transaction amount. These are our favorite transactions!</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><p style="text-align: center;"><img class="aligncenter wp-image-5579 size-full" src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/10/blog_reference_wallet_txns.png" alt="" width="1521" height="604"></p></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>The <a href="https://z.cash/upgrade/sapling/">Sapling network upgrade</a> — released Oct. 28 — greatly improved the performance of creating these shielded transactions. &nbsp;Prior to this upgrade, shielded addresses were too computationally intensive to run on a mobile device, and could only be accessed via a full node client. Now that it is possible for mobile devices to support shielded addresses, we want to encourage the community to support them. &nbsp;</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Reference wallet</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p><p>Our reference wallet has a minimal number of features, and for a reason: It is not designed to be an end user application, but rather a resource. The reference wallet’s goal is to deliver a light client example that focuses on Sapling shielded interactions, leverages a zcashd full node as a server in a privacy-preserving way, and consumes the native rust implementation of Zcash wallet components. The reference wallet secondarily also serves as a design example of a single-currency application that only uses shielded addresses and leverages Zcash-specific features not commonly supported by multi-currency wallets.</p>
<p style="text-align: center;"><img class="aligncenter wp-image-5581" src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/10/blog_reference_wallet_mobile_960w.png" alt="" width="480" height="272"></p></p>
<!-- /wp:paragraph -->
<!-- wp:image /-->
<!-- wp:paragraph -->
<p>Given the technical challenges associated with implementing shielded addresses, the most obvious but non-privacy preserving way for a light client to interact with a server is to give the server its <a href="https://z.cash/blog/viewing-keys-selective-disclosure/">viewing key</a>. Then, the server can see which transactions belong to a particular shielded address and pass those relevant transactions along. However, we don’t find this to be a satisfying solution because it does not meet our privacy goals:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>The server should not learn which transactions belong to a given wallet.</li><li>The server should not learn which transactions are being spent by a given wallet.</li></ul>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>We are working on an initial solution that preserves the privacy of the light clients. For instance, we pre-process blockchain information so that a wallet can feasibly scan through it itself to look for incoming transactions, but more efficiently than if it had to download the raw blocks and try decrypting them in a naive way.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We have already started work on the reference wallet, and we plan to share our progress and all resulting design and code in a series of forthcoming blog posts.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Coming up</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>A series of blog posts will feature specific areas of the reference wallet work: &nbsp;&nbsp;</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>Design: user experience priorities, user interface design, and styling choices</li><li>Protocol: technical challenges, interacting components, and privacy goals</li><li>Implementation: target devices, build methodology, and security measures</li></ul>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>Come back to <a href="https://z.cash/blog/">the Zcash blog</a> or follow us on <a href="https://twitter.com/electriccoinco">Twitter</a> for further updates!</p>
<!-- /wp:paragraph -->