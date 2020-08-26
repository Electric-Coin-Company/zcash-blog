---
ID: 4987
post_title: >
  New Empirical Research into Zcash
  Privacy
post_name: new-research-on-shielded-ecosystem
post_date: 2017-12-04 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-research-on-shielded-ecosystem/
published: true
tags:
  - privacy
  - transactions
categories:
  - General
---
<p>A researcher from University of Michigan-Dearborn, Jeffrey Quesnelle, published a <a class="reference external" href="https://arxiv.org/abs/1712.01210">paper</a> and <a class="reference external" href="http://jeffq.com/blog/on-the-linkability-of-zcash-transactions/">blog</a> today about the effective privacy on the Zcash blockchain over the first year of its existence. No vulnerabilities in Zcash were uncovered in this research. However, the research underscores a specific way that Zcash — like any other financial privacy technology — can fail to protect you if you use it the wrong way.</p>
<p>To recap, in Zcash there are both “shielded” and “transparent” addresses. Zcash stored in transparent addresses is visible in the blockchain to everyone. Zcash stored in shielded addresses is not.</p>
<p>The way that you can use this the wrong way is to move a certain amount of money into a shielded address, and then move that same amount out again. As we described in a <a class="reference external" href="/blog/transaction-linkability#linking-values">blog post</a> in January:</p>
<div class="figure align-center"><img class="center-image high-res-image" src="/wp-content/uploads/2017/12/z-linkability.png" alt="A diagram showing the possibile value linkability in a transaction series even when a shielded address is used in between transparent addresses"></div>
<p>An observer can deduce the money that Alice sent must have been transferred to Carol. This same issue can arise with any financial privacy technique, for example if you have some Bitcoin, and you Shapeshift it to a privacy coin and then Shapeshift it back to Bitcoin.</p>
<p>Jeffrey Quesnelle’s paper examined the Zcash blockchain to search for patterns of usage like this. To summarize the findings, he identified a total of 10,946 transaction pairs appearing to be this pattern, accounting for 31.9% of coins being shielded. Our analysis of <a class="reference external" href="http://jeffq.com/zcash-rtts.htm">the list of transactions he published</a> indicates that 84.64% of the transactions were shielding newly-mined coins, meaning that the first transaction of the pair was sent by a miner or mining pool. The Zcash protocol requires that newly-mined coins must be shielded before they can be sent to a transparent address. The fact that these coins were subsequently deshielded suggests that the recipients opted to receive their mining payouts at a transparent address.</p>
<p>In other words, it’s not that these coins were being shielded because the sending user sought privacy but because they are forced to shield and deshield the coins by the Zcash protocol in order to send them to another transparent address. The paper rightly cautions against users expecting strong privacy when they receive funds sent from a z-address into their t-address. If users want the best privacy, they should always receive and store funds in a z-address.</p>
<p>The other 15.36% of the observed pattern of usage are potentially by people who didn’t understand that shielding and then deshielding your Zcash doesn’t provide strong privacy.</p>
<p>To protect yourself from this sort of exposure, <em>don’t think of shielded addresses as something you</em> <strong>pass money through</strong>, <em>think of them as something you</em> <strong>store money in</strong>. Storing money in a shielded address and sending a portion of it out as needed gives you very strong privacy. Moving money into it and then immediately moving that money out again does not. (The same goes for using other financial privacy technologies such as the aforementioned example of Shapeshifting to a privacy coin and back.)</p>
<p>This kind of empirical scientific research is absolutely necessary to help scientists and creators learn what works and what doesn’t, and how to protect users. Previous examples of this kind of scientific research include the <a class="reference external" href="https://monerolink.com/">Monerolink</a> paper and the <a class="reference external" href="https://drive.google.com/file/d/0B7e8g-wJId8md3FYUGF0TlB5NjQ/view">paper from the National University of Singapore</a>. The Zcash Foundation has recently <a class="reference external" href="https://z.cash.foundation//blog/grant-awards/">awarded a grant</a> to a team of scientists from the University of Luxemborg to further study the Zcash blockchain. This new paper by Jeffrey Quesnelle is an excellent piece of research, which adds significantly to the scientific understanding of the real-world effects of privacy technologies. We'd like to express our thanks to him for doing this research.</p>
<p>We welcome and encourage this kind of research into Zcash’s privacy properties, and encourage anyone who is undertaking it to reach out to us if we can assist in any way. Also, please notify us in case your results might imperil users and notifying us about them in advance can help us protect Zcash users.</p>
