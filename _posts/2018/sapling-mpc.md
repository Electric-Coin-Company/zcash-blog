---
ID: 5012
post_title: Announcing the Sapling MPC
post_name: sapling-mpc
post_date: 2018-05-22 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/sapling-mpc/
published: true
tags:
  - Parameter Generation
  - Sapling
categories:
  - Technical
---
<p>Zcash's shielded transactions rely on zk-SNARKs <span class="ILfuVd yZ8quc">— small, fast-to-verify zero-knowledge proofs of arbitrarily complicated statements. These proving schemes rely on a set of public parameters that can be used to create and verify proofs for specific computations or "circuits". Any time we change our construction, we'll need to create new parameters.</span></p>
<p>It's important that these parameters be constructed securely in order to prevent counterfeiting. In our initial "Sprout" launch of Zcash, we performed a cryptographic ceremony to construct the parameters. We wanted to do better for our upcoming "Sapling" network upgrade, so we're using a <a href="https://eprint.iacr.org/2017/1050">new multi-party computation (MPC) protocol</a> to make the process more transparent and secure.</p>
<p>The protocol works in two phases:</p>
<ol>
<li><strong>The Powers of Tau</strong>: This phase produces parameters that anyone can use for their projects because they're agnostic to the circuit. This phase has already completed and was a smashing success! <a href="https://z.cash.foundation//blog/conclusion-of-powers-of-tau/">You can read about it here.</a></li>
<li><strong>Sapling MPC</strong>: We can use some of the results of the Powers of Tau, but we still need to produce the circuit-specific portions of the parameters. This MPC will focus on producing those.</li>
</ol>
<p>Each of these phases has the property that only <em>one</em> of its participants must be honest for the final parameters to be secure. Each phase is also highly scalable, allowing us to have as many participants as time allows. This means that we can open the doors to anyone who wants to contribute!</p>
<h2>Contributing</h2>
<p>Contributing to the Sapling MPC is easy. If you're interested, please email <strong>mpc@z.cash</strong> and we'll arrange a time for you to contribute. When it's your turn, you'll receive a file called <strong>params</strong>. You'll run a computation on this file using a <a href="https://github.com/zcash-hackworks/sapling-mpc">Rust-language program</a> we've written. When it's done, it'll print out a hash that you should keep for later verification. It will also produce a new file called <strong>new_params</strong> which you'll upload back to us.</p>
<p>There are no restrictions on what participants can do during their part in the ceremony. If you trust your machine and all this code, then the process is easy. But if you don't trust the code or your compiler or even your machine, you're encouraged to keep track of what compiler binaries you use, the git commit of the code you're running, and any other information that could be valuable for post-hoc analysis.</p>
<p>We'll be updating this page with more information such as alternative implementations of the code or other utilities and techniques that can be used to improve the security of contributions.</p>
