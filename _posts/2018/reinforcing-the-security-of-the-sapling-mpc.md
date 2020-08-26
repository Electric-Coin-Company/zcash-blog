---
ID: 5665
post_title: >
  Reinforcing the Security of the Sapling
  MPC
post_name: >
  reinforcing-the-security-of-the-sapling-mpc
post_date: 2018-11-16 14:05:05
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/reinforcing-the-security-of-the-sapling-mpc/
published: true
tags:
  - Sapling
  - zkSNARKs
categories:
  - General
---
<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">The engineering and cryptography team at Zcash makes very large efforts to minimize risk. This is always a positive thing, but perhaps even more crucial when using very new cryptography. Auditing is an important tool for this. One of the auditors we hired is Mary Maller,&nbsp;a Ph.D. student of Sarah Meiklejohn and Jens Groth at University College London—and currently one of the leading experts in the world on zk-SNARKs. In this post we announce an <a href="https://github.com/zcash/sapling-security-analysis/blob/master/MaryMallerUpdated.pdf">independent proof of security</a> by Mary for a crucial component in the Sapling upgrade:&nbsp;The <a href="https://z.cash/blog/new-mpc-protocol/">MPC protocol</a> that was used to generate the zk-SNARK parameters.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">The protocol was initially presented in a <a href="https://github.com/arielgabizon/sapling-security-analysis/blob/master/secondmpc.pdf">paper</a>&nbsp;[BGM] of Sean Bowe, Ian Miers and I. Mary's work gives us an additional independent data point that the MPC protocol and zk-SNARK we are using are provably secure.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">The zk-SNARK in Sapling was designed by Jens Groth <a href="https://eprint.iacr.org/2016/260">[Groth16]</a>. However, the structure of [Groth16]'s parameters doesn't allow for them to be computed in an MPC without* the players exposing their secret randomness. For this reason [BGM] looks at a version of [Groth16] where auxiliary elements are added to the SNARK parameters to make them more "MPC friendly"—these are exactly the elements that were computed in the <a href="https://z.cash.foundation/blog/powers-of-tau/">Powers of Tau</a> ceremony.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">[Groth16] proves SNARK security in what is called the <em>Generic Group Model.</em>&nbsp;[BGM] proves access to these auxiliary elements does not give such a generic group adversary any additional power to create fraudulent proofs. Independently verifying that adding these elements to the parameters does not break the zk-SNARK security was the original scope of Mary's work; this is a most crucial point where we are very happy to have independent verification.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Her paper continues by showing, using different methods than [BGM], that a party controlling all but one of the participants in each round of the MPC (i.e. both in the Powers of tau ceremony and the subsequent <a href="https://z.cash/blog/completion-of-the-sapling-mpc/">Sapling MPC</a>) does not gain advantage afterwards in producing fraudulent proofs. Her proof has the advantage of being simpler than [BGM] and not requiring a random beacon - a source of randomness whose value can be relied on not to be known up to a certain point in time (in our MPC we used [latex]2^{42}[/latex] repetitions of SHA-256 on a bitcoin block header for this). This random beacon is essential for the security proof of [BGM] whose MPC part requires mainly the Knowledge of Exponent assumption. Mary shows that if you further assume the adversary is a generic group adversary (something needed in any case for proving the [Groth16] SNARK secure) the random beacon is not required. Thus, an additional benefit from this work is showing the Sapling MPC is secure in the generic group model even in case the random beacon was compromised.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We plan to release a number of audit results related to the Sapling and Overwinter network upgrades soon. Keep an eye on this blog for those results and announcements of plans for future contracted security audits.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>*<em>In general, any multivariate function can be computed in a secure MPC; but the type of efficient MPC we use for SNARK parameters requires functions computed by circuits where every multiplication gate is an output gate. This style of MPC started in <a href="https://www.ieee-security.org/TC/SP2015/papers-archived/6949a287.pdf">this work</a>.</em></p>
<!-- /wp:paragraph -->