---
ID: 5051
post_title: Sapling in HD
post_name: sapling-in-hd
post_date: 2018-10-26 13:59:03
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/sapling-in-hd/
published: true
tags:
  - bitcoin
  - explainers
  - features
  - Sapling
  - wallets
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>Broader ecosystem adoption of shielded addresses through&nbsp;the implementation of&nbsp;<a href="/blog/cultivating-sapling-faster-zksnarks/">faster zk-SNARKs</a>&nbsp;has been a&nbsp;highlight of the <a href="https://z.cash/upgrade/sapling">Sapling network upgrade</a>. However, there are supplemental enhancements introduced for Sapling shielded addresses which further optimize efficiency and usability. The implementation of shielded HD wallets is one key feature.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>HD Wallets for Bitcoin and Transparent Addresses</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Before launch, the Zcash engineering team decided to keep a Bitcoin-like address functional in the protocol in order to allow for easier adoption by third-party services. These <em>transparent</em> addresses have been not only useful to avoid the resource requirements of legacy shielded addresses; they also support many advanced features already developed for Bitcoin.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Since the launch of Zcash, a number of services have implemented transparent addresses within their&nbsp;<em>HD wallets</em>, a feature initially proposed for Bitcoin in 2012. These HD wallets derive private keys and addresses from a&nbsp;<em>seed,&nbsp;</em>often a sufficiently randomized set of words. This means users can backup and fully restore an entire wallet with just a set of words.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Without this feature, users are required to do regular backups of the wallet as new addresses are created within it to protect against the loss of funds. Zcashd users should be familiar from the&nbsp;<a href="https://zcash.readthedocs.io/en/latest/rtd_pages/wallet_backup.html">wallet backup documentation</a>&nbsp;provided for legacy shielded addresses and transparent addresses.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>HD Wallets for Sapling Addresses</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Engineers at Zcash Company have developed an HD wallet specification for shielded addresses. <a href="https://github.com/zcash/zips/blob/master/zip-0032.rst">ZIP 32</a>&nbsp;details how this is implemented.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5517,"align":"center","width":488,"height":563} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/10/sapling-keys-and-addresses-3.png" alt="" class="wp-image-5517" width="488" height="563"/></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>The diagram above illustrates the basic implementation of Sapling's shielded HD wallet. Access to the seed will allow that party to derive the entire tree of keys in the wallet. The seed first establishes a pair of master keys; this pair consists of a master <em>spend key</em> and a master <em>view key</em>. Access to the master spend key is equivalent to knowing the seed. For an introduction to view key concepts, read the post <a href="https://z.cash/blog/viewing-keys-selective-disclosure/">Selective Disclosure &amp; Shielded Viewing Keys</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Accounts and Address Management</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p><p>Next, the master keys establish distinct accounts with their own private key pairs (spend and view). Access to account keys restricts spending or viewing capabilities to only that account.&nbsp;The account's view key derives the shielded address used for receiving payments. The Sapling protocol also allows deriving multiple addresses under the control of a single spend and view key pair. We'll write more about this feature down the road.</p>
<p>As explained in the post&nbsp;<a href="https://z.cash/blog/shielded-address-contexts/">Payment Contexts &amp; Reusing Shielded Addresses</a>, the properties of shielded addresses allow users to safely reuse them without risking transaction linkability. As a result, most individual users will not need more than one or two account keys. Businesses, on the other hand, might have distinct budgets with distinct managers and using these accounts can delineate authority over budgets while maintaining an executive authority over the master keys.</p></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We're looking forward to the Zcash ecosystem taking advantage of the new features introduced in Sapling in the coming months. If you have questions about supporting Zcash in your service, reach out to the <a href="mailto:ecosystem@z.cash">ecosystem team</a> or <a href="https://chat.zcashcommunity.com">ask in the community</a>.</p>
<!-- /wp:paragraph -->