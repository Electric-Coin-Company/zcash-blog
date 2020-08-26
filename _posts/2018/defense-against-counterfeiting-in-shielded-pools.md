---
ID: 5668
post_title: >
  Defense Against Counterfeiting in
  Shielded Pools
post_name: >
  defense-against-counterfeiting-in-shielded-pools
post_date: 2018-11-13 22:02:51
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/defense-against-counterfeiting-in-shielded-pools/
published: true
tags:
  - Policies
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>Zcash private addresses and transactions ensure that users are protected from the watchful eye of those wishing to exploit the use of data generally made available on public blockchains. This comes with certain risks. For example, there are limited means to immediately detect a bug in a zk-SNARK circuit that allows an attacker to counterfeit coins.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>That said, we are able to detect whether that counterfeiting has occurred by using the expected shielded pool totals. ZEC is created by miners into transparent addresses, and subsequently shielded, which increases the total ZEC in that pool. The pool total decreases when ZEC held in shielded addresses is spent to unshielded addresses. If the total goes negative, we know that counterfeiting has taken place.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Upon detecting this condition, the Zcash Company would begin its investigation into the possible source of the vulnerability as well as which pool, or pools, are affected. If we are able to identify that the bug affects only a single shielded pool, we might choose to effectively deactivate that pool by invalidating any of its outgoing transactions. A necessary consequence of this action is that any legitimate funds would also be lost forever in the affected pool. <br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Once the bug has been identified and remediated, Zcash nodes would be okay to resume normal operation. While these actions would be quite disruptive to the network, they are necessary for the long term viability of Zcash and for the safety of its users.<br /></p>
<!-- /wp:paragraph -->