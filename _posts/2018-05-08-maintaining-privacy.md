---
ID: 3084
post_title: Maintaining Privacy
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/maintaining-privacy/
published: true
post_date: 2018-05-08 17:10:38
---
We support science. Open scientific investigation is the only way for developers to learn what works and what doesn't work to protect users and fulfill our mission. 

Today, George Kappos, Haaroon Yousaf, Mary Maller, and Sarah Meiklejohn from University College London released new academic research entitled “<a href="https://smeiklej.com/files/usenix18.pdf">An Empirical Analysis of Anonymity in Zcash.</a>" We congratulate this research team for this insightful new paper, and invite other scientists to join with us in investigating these questions that are important to the future of human society.

This research demonstrates different ways to pierce the veil of your privacy if you, or the people that you transact with, move money from a transparent address to a shielded address and then move some of that money back to a different transparent address. <a href="https://blog.z.cash/new-research-on-shielded-ecosystem/">Similar analysis</a> was released several months ago. However, this research includes new techniques that can heuristically link patterns of “unshielded to shielded to unshielded” transactions.

It is valuable to understand how much privacy is lost when using shielded addresses as a pass-through mechanism, but using it in that way is not recommended. Instead, store your Zcash in a shielded address. When paying someone, send Zcash from your shielded address to their shielded address. If Zcash is transacted in this way, the results of this paper do not apply and transaction privacy is maintained.

We recognize that it is common to use transparent addresses for transactions and we need greater shielded address adoption. That is why our current priority is to launch the Zcash Sapling upgrade, scheduled for activation in September of this year, making shielded addresses so efficient that every cryptocurrency exchange, software wallet, hardware wallet, merchant, and product can support shielded addresses as the primary means to send and receive Zcash. It is imperative that a <a href="https://blog.z.cash/shielded-ecosystem/">shielded ecosystem</a> be established to ensure the future of Internet Money.

<strong>Update:</strong> Since we posted this blog, the team behind this research <a href="https://www.benthamsgaze.org/2018/05/09/the-pools-run-dry-analyzing-anonymity-in-zcash/">released a blog post</a> that nicely summarizes their findings.

<b>Please note that this blog post addresses the specific research in this paper. Users concerned with how to use Zcash safely should see our <a href="https://z.cash/support/security/privacy-security-recommendations.html">privacy and security recommendations</a>.</b>