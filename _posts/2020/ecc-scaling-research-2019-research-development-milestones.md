---
ID: 9312
post_title: 'ECC scaling research:  2019 research &#038; development milestones'
post_name: >
  ecc-scaling-research-2019-research-development-milestones
post_date: 2020-03-02 14:47:57
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/ecc-scaling-research-2019-research-development-milestones/
published: true
tags:
  - Halo
  - L1 scalability
  - sharding
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>Scaling is a central discussion for blockchain teams and a critical issue that needs to be addressed as this technology matures. ECC has spearheaded groundbreaking research in this area, focusing primarily on layer 1 scalability. In this post, we’ll explain the importance of layer 1 scalability and summarize our research in this area.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Why is L1 scalability important?&nbsp;</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Scalability solutions are designed to help blockchain networks maintain transaction throughput and low transaction fees as the network grows. Researchers have proposed a variety of potential solutions — from layer 1 approaches like sharding or proof-of-stake to layer 2 approaches like side-chains or off-chain computations.&nbsp;&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The <a href="https://en.wikipedia.org/wiki/Lightning_Network" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Lightning Network</a> and <a href="https://boltlabs.tech/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">BOLT</a> are examples of layer 2 scalability solutions that enable payment channels to hold funds in escrow until one or more parties is ready to cash out. While layer 2 solutions are critical for ecosystem development, we believe that privacy must be protected at the base layer, or layer 1, in order to ensure consistent usability, fungibility, censorship resistance and a viable medium of exchange across all use cases.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Layer 1 scalability requires horizontal scalability, where the network scales as infrastructure providers contribute additional resources. Said another way, horizontal scalability means that as infrastructure is added, network capacity increases.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If Zcash is for everyone, we must scale layer 1 as usage grows. Some of this research has practical applications today, while some of it is speculative with a long-term vision for the future. </p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Summary of our work in 2019</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Horizontal scalability and usability goals</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>ECC’s CTO, Nathan Wilcox, presented his vision for <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.youtube.com/watch?v=tKGAs8RuZfk&amp;feature=youtu.be" target="_blank">Zcash at a global scale</a> at Zcon1. In order to scale Zcash to 10 billion users by 2050, he outlined two goals: usability continuity and ux-unobtrusive infrastructure. Usability continuity means that usability should not undergo qualitative changes as the network grows, <em>e.g.</em>, changes in transaction flows or fee mechanics. UX-unobtrusive infrastructure refers to infrastructure that does not impact a user’s decision-making. For example, users should not need to understand whether the sender and the recipient are in the same shard or even that shards exist.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Practical recursive ZKPs with Halo</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In September 2019, ECC researcher Sean Bowe, along with Daira Hopwood and Jack Grigg, published <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/halo-recursive-proof-composition-without-a-trusted-setup/" target="_blank">Halo</a>, a paper detailing a new technique that allows for the creation of efficient, recursive zero-knowledge proofs. What does this mean in practice? With Halo, you can create a proof that verifies a prior instance of itself, a “proof of proofs” that allows you to compress any amount of data into a short proof that can be checked quickly. Not only does Halo avoid a trusted setup, but it also promises dramatic performance improvements, with proofs as small as 3.5 KiB. Halo research has been <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.coindesk.com/zcashs-halo-breakthrough-is-a-big-deal-not-just-for-cryptocurrencies" target="_blank">recognized as a breakthrough</a> not just for cryptocurrencies, but for the entire field of applied cryptography. Since September, Sean and team have been working to formalize Halo so it can undergo extensive peer review and security analysis. They have developed a high-performance implementation which demonstrates practical efficiency. We may see variants of Halo deployed in production on other projects as early as this year. Sean explained Halo in layman’s terms during ECC’s <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.youtube.com/watch?v=HX2AZcHZHBo" target="_blank">quarterly livestream</a> (starts at minute 22). <em>Please note, Halo is a work in progress and has not yet been peer-reviewed.</em></p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:image {"id":9318,"width":600,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/02/Halo-Sean-800x450.png" alt="" class="wp-image-9318" width="600"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Scaling privacy through sharding architecture</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Daira Hopwood presented <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.youtube.com/watch?v=RN82M_ShLtw&amp;feature=youtu.be" target="_blank">a research proposal</a> for sharding architecture at Zcon1 and again at the ZKP Amsterdam Community Event. Daira’s research proposal calls for the use of <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://en.wikipedia.org/wiki/Shard_(database_architecture)" target="_blank">sharding</a>, a technique that partitions a database into sections or “shards” to improve the throughput limit, in order to scale to high transaction volumes. Hir proposal uses recursive SNARK validation (similar to Coda) to create summaries of state updates and to allow clients to catch up almost instantly. To reduce the reliance on trusted setups, Daira proposes transparent SNARKs. And finally, Daira’s proposal also includes a mix-net to replace broadcast of transactions to miners and all potential token receivers, while maintaining privacy. See Daira’s slides <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/daira/scaling/raw/master/scalable-privacy-ams.pdf" target="_blank">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:image {"id":9325,"width":600,"sizeSlug":"medium"} -->
<figure class="wp-block-image size-medium is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/02/Sharding-Daira-2-800x450.png" alt="" class="wp-image-9325" width="600"/></figure>
<!-- /wp:image -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Capacity increase: Faster block times with Blossom</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Prior to investing in an ambitious architectural upgrade, less-disruptive capacity increases can satisfy current growth. Our latest network upgrade, <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/blossom-upgrade-improves-speed-scalability-capacity/">Blossom</a>, included an example of such a capacity increase: The block mining rate was doubled, allowing a higher rate of transaction confirmations, thus lowering fees and reducing confirmation times.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":38} -->
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>What to expect in 2020</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Our audacious goal is to bring Zcash to <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/zcash-to-10-billion/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">10 billion users</a>, and to that end, we have dedicated much of our long term protocol research efforts into making a future version of Zcash horizontally scalable for Sapling-equivalent private payments. This research is part of our overall <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/ecc-flight-plan-for-2020/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">flight plan for 2020</a> and beyond. We know these goals are ambitious and that some of this research might never make its way into a network upgrade. We know any layer 1 scalability upgrade will require support from the Zcash development community, one that grows more diverse by the week.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>While carrying out this far-reaching research, we also intend to develop a capacity plan to ensure there’s a common understanding of (1) how to measure usage and anticipate capacity limitations, (2) which different capacity improvements are plausible, and (3) what the respective risks and payoffs are. ECC wants to help the Zcash community prepare for network growth safely and effectively, well ahead of demand.&nbsp;<br></p>
<!-- /wp:paragraph -->