---
ID: 5059
post_title: Sapling Transaction Anatomy
post_name: sapling-transaction-anatomy
post_date: 2018-10-16 14:45:44
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/sapling-transaction-anatomy/
published: true
tags:
  - explainers
  - privacy
  - Sapling
  - sprout
  - transactions
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>With the Sapling activation approaching, we're continuing our education on what users and third-party services can expect. We recently <a href="https://blog.z.cash/sapling-addresses-turnstile-migration/">announced the Sapling turnstile</a> and what users should anticipate with this feature. In this post, we're going to look at the Sapling transaction anatomy.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Legacy Shielded Transactions and JoinSplits</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Just after the launch of Zcash, we wrote an introduction on the <a href="https://blog.z.cash/anatomy-of-zcash/">Anatomy of A Zcash Transaction</a>.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":1667,"align":"center","width":521,"height":350} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2016/11/basic-txn-types_v2.png" alt="Basic Zcash spend types include public, shielding, deshielding and shielded" class="wp-image-1667" width="521" height="350"/></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>The basic spend types will also apply after Sapling activation but there are some nuanced changes to how shielded addresses appear in transactions. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>In transactions involving legacy shielded addresses, the zero-knowledge proof operation is referred to as a <em>JoinSplit</em>. A JoinSplit consumes either one or two input values and creates either one or two output values. These input and output values are referred to as <em>notes</em>.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>A JoinSplit does not reveal whether one or two notes were actually consumed or created. A transaction requiring the consumption or creation of more than two notes uses multiple JoinSplits.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5405,"align":"center","width":583,"height":256} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/09/multiple-joinsplits-txn-1.png" alt="Explorer view of a multiple joinsplit transaction" class="wp-image-5405" width="583" height="256"/></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>The <a href="https://zcash.blockexplorer.com/tx/4dccd4e296fabd1a597968aeedf8158fec6c49f1b650f3ddbbc12298b0467e5a">transaction above</a> shows a fully-shielded payment requiring multiple JoinSplits. You don't get much information from this other than the transaction consumed or created many notes.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Sapling Shielded Transactions</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Due to the efficiency improvements in Sapling, shielded transactions using the new Sapling addresses look slightly different. They still consume and create notes but do not employ JoinSplit operations. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Instead, the new Sapling operation is composed of spends and outputs.&nbsp; These include detail on the exact number of notes consumed or created in transactions.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>To compare, take a look at a testnet <a href="https://explorer.testnet.z.cash/tx/abbd823cbd3d4e3b52023599d81a96b74817e95ce5bb58354f979156bd22ecc8">Sapling transaction</a>:</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5407,"align":"center","width":581,"height":171} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/09/testnet-sapling-txn-1.png" alt="Explorer view of a testnet Sapling shielded transaction" class="wp-image-5407" width="581" height="171"/></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>Notice that the explorer shows one shielded spend (consumed note) and two shielded outputs (created notes). </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>It's likely that this transaction consumed a note to send part of its balance to another address and the remainder as change sent back to the original address. However, they may have sent their entire note balance to two addresses and had no change. We can't know for sure.</p>
<!-- /wp:paragraph -->
<!-- wp:image {"id":5406,"align":"center","width":579,"height":177} -->
<div class="wp-block-image"><figure class="aligncenter is-resized"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/09/testnet-sapling-from-t-txn-1.png" alt="" class="wp-image-5406" width="579" height="177"/></figure></div>
<!-- /wp:image -->
<!-- wp:paragraph -->
<p>If a sender, Alice, needed to create a payment which sent a single Sapling shielded address the entire balance from her transparent address (perhaps she is completing a <a href="https://blog.z.cash/sapling-addresses-turnstile-migration/">Sapling turnstile migration</a>), then the explorer would show zero shielded spends and 1 shielded output.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>User Impacts</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>We do not think the change in transaction anatomy should directly impact how Sapling shielded addresses are used but we do think it's important for users to be aware, no matter how minor of an effect.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For example, services tracking Zcash blockchain activity such as block explorers will be able to distinguish the type of shielded address used (legacy vs Sapling). They could even add new labels to the interfaces so users can distinguish as well.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Everything else about shielded transactions remains the same including value, address and the memo remaining protected and transaction fees remaining visible.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Stay tuned for our next post on what users should expect with the Sapling activation. If you have any questions about Sapling transaction anatomy, we recommend bringing them to the community <a href="https://chat.zcashcommunity.com">chat</a> or <a href="https://forum.zcashcommunity.com">forum</a>.</p>
<!-- /wp:paragraph -->