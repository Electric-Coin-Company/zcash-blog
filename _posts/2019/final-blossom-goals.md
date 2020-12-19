---
ID: 6143
post_title: Final Blossom Goals
post_name: final-blossom-goals
post_date: 2019-01-15 21:17:15
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/final-blossom-goals/
published: true
tags:
  - Blossom
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>Since <a href="https://forum.zcashcommunity.com/t/announcing-zcash-blossom-and-proposed-feature-goals/31891">announcing the proposed Blossom goals on the Forum</a> this past November, the Zerocoin Electric Coin Company has worked both internally and across the wider community to gather information and capacity-plan in order to achieve the proposed Blossom goals. We solicited and received feedback from the community; thank you for your passion, thoughtfulness and attention to detail.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Following this process, we’ve narrowed down the Blossom goals and further refined them. This is the resulting final list of goals for what the Company will implement and support in the Blossom series of its <em>zcashd</em> software:</p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol><li><a href="https://github.com/zcash/zcash/issues/3673">Split Founders' Reward</a>: The Blossom series of <em>zcashd</em> will decouple the three funding streams for <a href="https://z.cash.foundation/">the Zcash Foundation</a>, Company Strategic Reserve, and the remainder. This will help to de-risk these funding streams, as previously they were all running through one stream. The current model of a single revenue stream runs the risk of being compromised, whether it is carried out by hackers, the result of a legal issue, a technical mistake of some kind, or organizational failure. In the existing model in any of these scenarios, all three revenue streams could be compromised. In this new model where we split the founders’ reward in the protocol, revenue streams that are not directly compromised will be left unaffected, akin to the notion of “reducing the blast radius” of an event.</li><li><a href="https://github.com/zcash/zcash/issues/3690">Shorter Blocktimes</a>: The Blossom series of <em>zcashd</em> increases the frequency of blocks (subject to further security and performance analysis), allowing more transactions and allowing them to resolve faster. This will improve Zcash’s usability and increase how many transactions per hour the network can sustain while keeping transaction fees low.</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>You’ll notice that <a href="https://github.com/zcash/zcash/issues/3672">Harmony Mining</a> is no longer on the list of goals for Blossom. During the R&amp;D phase, we determined that the unresolved security and engineering issues of Harmony Mining could not be solved in the Blossom timeline. As a result we are <a href="https://github.com/zcash/zcash/issues/3672#issuecomment-453891932">postponing this goal to NU3</a>, the upgrade occuring after Blossom in April 2020.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>As a note, there are three more points along the network upgrade timeline below where we may need to abort any of these goals if we find significant issues with our approaches: </p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol><li>As a result of specification auditing (end of February) </li><li>Inability to finish the code on-time (end of March)</li><li>Code auditing or testing (end of May)</li></ol>
<!-- /wp:list -->
<!-- wp:image {"id":6148,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/01/zcash_network-upgrade_process_timeline.png" target="_blank" rel="noreferrer noopener"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/01/zcash_network-upgrade_process_timeline-1024x460.png" alt="" class="wp-image-6148"/></a></figure>
<!-- /wp:image -->
<!-- wp:heading {"level":3} -->
<h3>Possible Regular Releases</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>In addition to the network upgrade goals above, the Company will be pursuing the following goals as possible regular releases. Given the limited time and engineering resources available between now and May 31st, when the code needs to be released for the Blossom upgrade, we shifted any goals able to be achieved (even in part) with a regular release outside of the Blossom network upgrade.<br /></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>These goals are targeted as part of regular releases before Blossom activation at the end of October:</p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol><li><a href="https://github.com/zcash/zcash/issues/3677">Sprout Address Retirement</a>: We plan to create a standard rule to disallow sending funds to a Sprout address. We will include this as part of a consensus change at a later date;</li><li><a href="https://github.com/zcash/zcash/issues/3678">Rollback Protection</a>: We plan to put protections in place to mitigate the risks of rollbacks. This is a complex goal that will require a good amount of security analysis and discussion.</li></ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>The team has begun writing specifications for the two Blossom upgrade goals, as outlined at the top of this post, and is aiming to complete the specifications by January 22. The team plans to begin work on the additional regular release goals listed over the next 2-5 months. Stay tuned for further updates as we move forward on the Blossom upgrade schedule.<br /></p>
<!-- /wp:paragraph -->