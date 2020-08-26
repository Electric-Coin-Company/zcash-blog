---
ID: 9687
post_title: Explaining viewing keys
post_name: explaining-viewing-keys
post_date: 2020-05-18 19:41:41
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/explaining-viewing-keys/
published: true
tags:
  - features
  - privacy
categories:
  - General
  - Privacy
  - Technical
---
<!-- wp:paragraph -->
<p>Viewing keys, detailed in <a href="https://zips.z.cash/zip-0310" target="_blank" rel="noreferrer noopener">ZIP 310</a>, enable the separation of spending and viewing permissions for Zcash shielded addresses. By creating a separate viewing key, Zcash users can share visibility of the transactions sent and received from their shielded address without compromising their private spend key. This capability was added to the protocol in the Sapling network upgrade, and RPC support was released in <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-1-2/">version 2.1.2</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Shielded addresses allow Zcash users to transact while revealing as little information on the public blockchain as possible. This protects users' privacy from bad actors and business competitors. There are instances; however, where it is necessary to reveal some information to a third party, such as for audit or compliance purposes.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Viewing keys are a critical component of the Zcash value proposition because they allow users to selectively disclose information about their transactions.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":33} -->
<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:image {"id":9690,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/05/viewing-keys-illustration-800x400.png" alt="" class="wp-image-9690"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":33} -->
<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>For shielded transactions in Zcash, viewing keys are derived directly from a user's spending key. There is no central authority that controls access to viewing keys. Once a viewing key is created, it can only be obtained from someone who holds it. If you don’t give your viewing key out, then no one can access it without your participation.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Zcash protocol is designed with two features to support the disclosure of information:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Viewing keys</strong> provide visibility into the transaction value, memo field, and target address of all transactions received by or sent from a specific shielded address.</li><li><strong>Payment disclosure</strong> provides similar visibility for a single transaction. It is a method of proving that a payment was sent to a shielded address, without revealing all of the transactions sent to/from that address.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>These features enable owners of a shielded address to share transaction visibility in a secure and confidential manner. For cryptocurrency service providers, this means the ability to verify transactions to/from shielded addresses, while keeping spending authority keys on secure hardware, such as HSMs.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Viewing key use cases</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Viewing keys enable a variety of commercial use cases for Zcash that support completely private z-to-z transactions. A merchant might share their payment address viewing key with their accountant to track sales revenue; or a charity may publish their viewing key to verify contributions for donation matching.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Consider the following examples:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>An exchange wants to detect when a customer deposits ZEC to a shielded address, while keeping the “spend authority” keys on secure hardware (<em>e.g.</em>, HSMs). The exchange could generate an incoming viewing key and load it onto an Internet-connected “detection” node, while the spending key remains on the more secure system.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>A custodian needs to provide visibility of their Zcash holdings to auditors. The custodian may generate a full viewing key for each of their shielded addresses and share that key with their auditor. The auditor will be able to verify the balance of those addresses and review past transaction activity to and from those addresses.&nbsp;</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>An exchange may need to conduct due diligence checks on a customer who makes deposits from a shielded address. The exchange could request the customer’s viewing key for their shielded address and use it to review the customer’s shielded transaction activity as part of these enhanced due diligence procedures.&nbsp;</li></ul>
<!-- /wp:list -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Implications for Zcash</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Viewing keys help ensure Zcash remains at the forefront of regulatory compliance by providing a mechanism by which exchanges and custodians can accept shielded deposits while keeping shielded ZEC in secure cold storage. Viewing keys allow sharing visibility of shielded transactions with auditors and, where appropriate, with regulators. This ensures Zcash users have privacy from criminals and bad actors, but that exchanges and other virtual asset service providers can remain fully compliant while supporting shielded addresses.</p>
<!-- /wp:paragraph -->