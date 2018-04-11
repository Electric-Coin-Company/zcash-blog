---
ID: 1605
post_title: 'BLS12-381: New zk-SNARK Elliptic Curve Construction'
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/new-snark-curve/
published: true
post_date: 2017-03-11 00:00:00
---
Our team is continually working to improve the security, performance and usability of our privacy-preserving <a class="reference external" href="/zcash-private-transactions/">shielded transactions</a>. As we mentioned in our <a class="reference external" href="/the-near-future-of-zcash/">near future priorities</a> blog post, we are working on a collection of cryptographic improvements for the next version of Zcash named Sapling. One of our goals is to make shielded payments more efficient and less memory intensive. We also intend to improve the concrete security level of the elliptic curve construction that we use for our zk-SNARK proofs.
<div class="figure align-center"><img class="center-image" src="https://z.cash/images/curve-graph-sm.png" alt="The BLS12-381 curve." /></div>
I spent some time last month designing and implementing a new pairing-friendly elliptic curve construction that is optimal for zk-SNARKs at the 128-bit security level. The construction minimizes performance and usability costs while increasing our security margins.

The construction will appear in an upcoming paper by our scientists, where it will be accompanied by a more thorough description of the construction and how it was selected.
<h2>Barreto-Naehrig curves</h2>
Barreto-Naehrig (BN) curves are a class of <a href="/pairing-cryptography-in-rust/">pairing-friendly</a> elliptic curve constructions built over a base field :math:`\mathbb{F}_q` of order :math:`r`, where :math:`r \approx q`. Our current curve construction has :math:`q \approx 2^{254}`. Last year, <a href="https://ellipticnews.wordpress.com/2016/05/02/kim-barbulescu-variant-of-the-number-field-sieve-to-compute-discrete-logarithms-in-finite-fields/">Kim and Barbulescu presented</a> a variant of the Number Field Sieve algorithm which reduced a conservative <a href="#id2">[1]</a> estimate of the security level to around 110 bits based on a <a href="http://eprint.iacr.org/2016/1102.pdf">recent paper</a>.

It is possible to construct a new BN curve that targets 128-bit security, even according to this conservative estimate, by selecting a curve closer to :math:`q \approx 2^{384}`. However, the larger group order :math:`r` impairs the performance of multi-exponentiation, fast fourier transforms and other cryptographic operations that we need to perform efficiently in zk-SNARK schemes and multi-party computations. Additionally, the larger scalar field :math:`\mathbb{F}_r` makes keying material unnecessarily large.
<h2>Barreto-Lynn-Scott curves</h2>
Barreto-Lynn-Scott (BLS) curves are a slightly older class of pairing-friendly curves which now appear to be more useful for targeting this security level. Current research suggests that with :math:`q \approx 2^{384}`, and with an embedding degree of 12, these curves target the 128-bit security level. Conveniently, the group order for these curves is :math:`r \approx 2^{256}`, which allows us to avoid the performance and usability drawbacks that accompany a larger scalar field.
<h2>BLS12-381</h2>
In zk-SNARK schemes, we need to manipulate very large polynomials over the scalar field :math:`\mathbb{F}_r`. We can perform efficient multi-point evaluation/interpolation with fast fourier transforms, so long as we ensure :math:`\mathbb{F}_r` is equipped with a large :math:`2^s` root of unity.

As is <a href="https://eprint.iacr.org/2012/232.pdf">common</a>, we target a subfamily of these curves that has optimal extension field towers and simple twisting isomorphisms. In order to ensure Montgomery reductions and other approximation algorithms are space-efficient, we target :math:`r \approx 2^{255}` so that the most significant bit of :math:`r` (and :math:`q`) are unset with 64-bit limbs.

As usual, in order to optimize for pairing performance, we ensure the parameterization of the BLS curve has low Hamming weight. The curve we have ultimately chosen is named <strong>BLS12-381</strong> as :math:`q \approx 2^{381}`.

<div class="new-curve-blog line-block">
<div class="line">u = -0xd201000000010000</div>
<div class="line">k = 12</div>
<div class="line">q = 0x1a0111ea397fe69a4b1ba7b6434bacd764774b84f38512bf6730d2a0f6b0f6241eabfffeb153ffffb9feffffffffaaab</div>
<div class="line">r = 0x73eda753299d7d483339d80809a1d80553bda402fffe5bfeffffffff00000001</div>
<div class="line">E(Fq) := y^2 = x^3 + 4</div>
<div class="line">Fq2 := Fq[i]/(x^2 + 1)</div>
<div class="line">E'(Fq2) := y^2 = x^3 + 4(i + 1)</div>
</div>

<h2>Rust language implementation</h2>
I have begun working on an implementation of the construction in Rust as part of my <a class="reference external" href="https://github.com/ebfull/pairing">pairing</a> library. The library has the goal of being portable, standards compliant, and high performance. Due to the nature of zk-SNARK schemes, it is difficult to efficiently construct proofs in constant time, and so the library does not currently focus on side channel resistance.

Future blog posts will describe a number of techniques and tools that our scientists have devised for using this curve construction to optimize Zcash.

<table id="id2" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="https://z.cash/blog/new-snark-curve.html#id1">[1]</a></td>
<td>Menezes, Sarkar and Singh (<a class="reference external" href="http://eprint.iacr.org/2016/1102.pdf">http://eprint.iacr.org/2016/1102.pdf</a>) show 2^110 is a conservative estimate for the size of the space of polynomials that needs to be scanned for smooth polynomials. However, for the case q=p^12 relevant for BN curves there is no currently published efficient method for scanning this space. (Checking each polynomial separately for smoothness would result in total running time larger than 2^128.) Thus, to the best of our knowledge the most efficient currently known fully described algorithm for breaking the curve Zcash is presently using is Pollard's rho, which would run in time sqrt(q)~2^127. (Our thanks to Palash Sankar and Shashank Singh for helping understand their result.)</td>
</tr>
</tbody>
</table>