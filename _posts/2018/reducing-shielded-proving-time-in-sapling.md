---
ID: 5864
post_title: >
  Reducing Shielded Proving Time in
  Sapling
post_name: >
  reducing-shielded-proving-time-in-sapling
post_date: 2018-12-17 11:05:04
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/reducing-shielded-proving-time-in-sapling/
published: true
tags:
  - cryptography
  - explainers
  - hash functions
  - Sapling
  - zkSNARKs
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>Since the successful Sapling network upgrade, we have already seen an increased adoption of shielded addresses in the Zcash ecosystem. Services like <a href="https://www.zcashcommunity.com/mining/mining-pools/">mining pools</a> are beginning to offer shielded address payouts to customers. Further, the number of third-party desktop <a href="https://z.cash/wallets/">wallets</a> supporting shielded addresses is also rising. Looking ahead,&nbsp;<a href="https://z.cash/blog/introducing-the-zcash-reference-wallet/">shielded address light client support</a> will promote even wider adoption. This is just the beginning for Zcash’s mission toward <a href="https://z.cash/blog/shielded-ecosystem">a shielded ecosystem</a>.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>The increased adoption of shielded addresses is due to the underlying&nbsp;<a href="https://z.cash/blog/cultivating-sapling-faster-zksnarks/">advancements</a>&nbsp;of Zcash cryptographers. They have developed and implemented significant changes to the zero-knowledge proving mechanism in Sapling. Years of research and cryptographic design work have produced these improvements which build upon existing schemes and invent new ones. </p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Three improvements</h2>
<!-- /wp:heading -->
<!-- wp:image {"id":5865,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-overview.png"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-overview.png" alt="Proving time reduction from Sprout's 37 seconds to Sapling's 2.3 seconds" class="wp-image-5865"/></a></figure>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>In order to understand the advancements used to reduce proving time and memory costs, we can break down the overall implementation into three components.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>Bowe-Hopwood Pedersen Hash</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The first of these comes from Zcash cryptographers, Sean Bowe and Daira Hopwood. Their work improved the efficiency of the Pedersen hash function for use in Zcash’s zk-SNARK circuit. </p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5866,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-1.png"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-1.png" alt="Proving time reduction of 75% in Sapling due to replacing the zk-SNARKs hashing function" class="wp-image-5866"/></a></figure>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>The majority of the zero-knowledge proof operation in shielded transactions consists of generating hashes. Therefore, an improvement here has a significant effect on the time requirements. By replacing the pre-existing SHA-256 hash with the new Bowe-Hopwood Pedersen hash, the time for shielded address payments in Sapling is already reduced by 75%. For details on this, refer to the <a href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">Zcash protocol specification</a> at section 5.4.1.7 “Pedersen Hash Function.” </p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>Bellman</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The second component we’ll consider is the zk-SNARK implementation, which involves two subcomponents. First is the elliptic curve construction and second is the proving system. The legacy implementation is <a href="https://github.com/zcash/libsnark">a Zcash fork of libsnark</a> which uses elliptic curve bn128 and the proving system described in <a href="https://eprint.iacr.org/2013/879.pdf">BCTV2015</a> (“Succinct Non-Interactive Zero Knowledge for a von Neumann Architecture”).</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5867,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-2.png"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-2.png" alt="Proving time reduction of 50% in Sapling due to replacing the zk-SNARKs circuit implementation from libsnark to bellman" class="wp-image-5867"/></a></figure>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>The zk-SNARK circuit implemented for Sapling uses a new elliptic curve construction, <a href="https://z.cash/blog/new-snark-curve/">BLS12-381</a>, which not only offers better performance but more security than the previous curve. This circuit also uses a more recent proving system as described in <a href="https://eprint.iacr.org/2016/260.pdf">Groth16</a> (“On the Size of Pairing-based Non-interactive Arguments”). Jens Groth’s system computes less than half of the number of proof elements compared to the original proving system. The Rust-language library, <a href="https://z.cash/blog/bellman-zksnarks-in-rust/">bellman</a>, applies these improvements which overall, offers another 50% increase in efficiency. Learn more about Zcash’s zk-SNARKs circuit on the <a href="https://z.cash/technology/zksnarks/">technology overview page</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:heading {"level":3} -->
<h3>Split Circuit</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The final of these is a split circuit design which replaces the use of JoinSplit transfers in legacy shielded addresses.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5868,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-3.png"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/12/proving-time-step-3.png" alt="Proving time reduction of 50% in Sapling due to implementing a split circuit design" class="wp-image-5868"/></a></figure>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>Not only does the split circuit design reduce computation time another 50% but it also allows for more granularity in generating a zk-SNARK for shielded address payments. The number of notes spent and created in a transaction determine the variation in proof creation time. This is also the reason that the <a href="https://z.cash/blog/sapling-transaction-anatomy/">transaction anatomy</a> is different in Sapling. For more details about the split circuit design, see section 3.6 of the <a href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">Zcash protocol specification</a> “Spend Transfers, Output Transfers, and their Descriptions.”</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Beyond Sapling</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Each of these components alone represent a significant achievement, so suffice it to say that together they deliver a <a href="https://z.cash/blog/sapling-activation-complete/">substantial victory</a>. The technological achievements produced for Sapling offer more than an upgrade to Zcash as well. Particularly the <a href="https://github.com/zcash/librustzcash/tree/master/bellman">bellman library</a> discussed above is a widely applicable tool for working with zk-SNARKs and we encourage other projects to explore the potential opportunities for its use. Keep an eye out for more documentation and don’t hesitate to reach out in the<a href="https://chat.zcashcommunity.com"> online community</a> if you’re interested in digging deeper.<br /></p>
<!-- /wp:paragraph -->