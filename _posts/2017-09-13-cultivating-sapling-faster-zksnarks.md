---
ID: 1555
post_title: 'Cultivating Sapling: Faster zk-SNARKs'
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/cultivating-sapling-faster-zksnarks/
published: true
post_date: 2017-09-13 00:00:00
---
<p>Zcash's next major upgrade, codenamed <a class="reference external" href="/the-near-future-of-zcash/">Sapling</a>, will feature a set of groundbreaking performance improvements for our shielded transactions. In the <a class="reference external" href="/cultivating-sapling-new-crypto-foundations/">last blog post</a> of this series, we talked about a new elliptic curve for zk-SNARKs called <a class="reference external" href="/new-snark-curve/">BLS12-381</a>, as well as new proving systems and other algorithms.</p>
<p>Matthew Green, Ian Miers and I are happy to announce that we have made significant performance improvements to the zk-SNARKs that Zcash uses. These improvements are being published open source, free of patents, for the broader crypto community.</p>
<div class="section" id="jubjub">
<h2>Jubjub</h2>
<p>We have designed an elliptic curve called <strong>Jubjub</strong> which is efficient to perform operations on inside of zk-SNARK circuits built over our new BLS12-381 curve. These kinds of "embedded" curves have been explored in previous works such as <a class="reference external" href="https://eprint.iacr.org/2015/1093.pdf">Kosba et al.</a> . We achieve record-breaking performance for fixed-based exponentiation.</p>
<p>Fast elliptic-curve cryptography in this context allows us to use more efficient primitives for commitment schemes and collision-resistant hashes. Combining the various techniques we've discussed in previous posts, we can get a rough idea of the performance improvements:</p>
<div class="figure align-center">
<img alt="Jubjub benchmarks" class="center-image" src="http://blog.z.cash/wp-content/uploads/2017/09/sapling-metrics.png"/></div>
<p>This rough estimate indicates an 80% reduction of proving time, and a 98% reduction in memory usage which is a key requirement for opening up mobile support for Zcash shielded addresses.</p>
<p>What's more, there are more optimizations and improvements that reduce these costs further that we plan to explore in future blog posts.</p>
</div>
<div class="section" id="technical-details">
<h2>Technical Details</h2>
<p>If you're interested in how Jubjub works, we've written an <a class="reference external" href="https://z.cash/technology/jubjub.html">explainer page</a>. We have also written an early <a class="reference external" href="https://github.com/Electric-Coin-Company/jubjub-prototype">prototype</a> to showcase and benchmark these new cryptographic primitives.</p>