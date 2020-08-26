---
ID: 4930
post_title: Pairing cryptography in Rust
post_name: pairing-cryptography-in-rust
post_date: 2016-07-06 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/pairing-cryptography-in-rust/
published: true
tags:
  - cryptography
  - Rust
  - zkSNARKs
categories:
  - Technical
---
<a class="reference external" href="https://en.wikipedia.org/wiki/Pairing-based_cryptography">Pairing cryptography</a> is an exciting area of research, and an essential component of Zcash's <strong>zkSNARKs</strong> — proofs that transactions are valid without requiring users to reveal private information. Earlier this year we also used zkSNARKs to make Bitcoin's <a class="reference external" href="/blog/science-roundup">first zero-knowledge contingent payment</a>!

One of our goals going forward is to better explain how these tools work, and to make them more accessible to the public. As a first step, we're starting development of a <a class="reference external" href="https://en.wikipedia.org/wiki/Pairing-based_cryptography">pairing cryptography</a> library for Rust called "bn". Pairing cryptography is important for zkSNARKs, but what exactly is it?
<h2>Elliptic Curves</h2>
Regular <a class="reference external" href="https://en.wikipedia.org/wiki/Elliptic_curve_cryptography">elliptic curve</a> constructions like <a class="reference external" href="http://www.secg.org/sec2-v2.pdf">secp256k1</a> — used in Bitcoin — are designed for things like <a class="reference external" href="https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm">digital signatures</a>. The points on the curve form a <a class="reference external" href="https://en.wikipedia.org/wiki/Cyclic_group">cyclic group</a>: they can be added together and multiplied by scalars. It is believed to be infeasible to find the multiplicand given a point and the product point, called the "elliptic curve discrete logarithm problem".

This asymmetry (the ease of multiplying but the difficulty of the reverse) is used to make a number of useful tools and protocols. Diffie-Hellman key exchange is a simple example: Alice multiplies Bob's public key by her (scalar) private key, and vice versa, to find a shared secret in the presence of an eavesdropper.

This key exchange protocol can be extended to three parties, but requires two rounds: for parties <cite>A</cite>, <cite>B</cite>, and <cite>C</cite>, <cite>A</cite> obtains the shared secret by having <cite>B</cite> send his public key to <cite>C</cite>, who multiplies it by her private key and sends the result to <cite>A</cite>, who can then derive the shared secret by multiplying it by her private key.
<h2>Pairing cryptography</h2>
Pairing cryptography is an extension of these concepts. Now imagine that we have <em>two</em> cyclic groups: :math:`G_{1}` and :math:`G_{2}`, written additively, and a mapping to a third cyclic group of the form e: :math:`G_{1} \times G_{2} \rightarrow G_{T}`, where :math:`G_{T}` is written multiplicatively. If this mapping is <em>bilinear</em>, then:

:math:`e(a g_{1}, b g_{2}) = e(g_{1}, g_{2})^{ab}` where :math:`a` and :math:`b` are scalars and :math:`g_{1}` and :math:`g_{2}` are generators for their respective groups.

Essentially, a scalar multiplication of one of the first two group elements is equivalent to an exponentiation of the final group element.
<h2>Joux's key agreement protocol</h2>
Let's apply pairing cryptography to the three-party key exchange scenario above. Using pairings, we can perform the exchange in <em>one round</em>. Each party :math:`P` publishes their public key :math:`P^{pk} = (P^{sk} g_{1}, P^{sk} g_{2})` and keeps their private key :math:`P^{sk}` secret. All of the parties :math:`A, B, C` can compute the same shared secret using the bilinear pairing function:
<table class="docutils table table-responsive"><colgroup> <col width="33%" /> <col width="33%" /> <col width="33%" /> </colgroup>
<thead valign="bottom">
<tr>
<th class="head">Alice Computes</th>
<th class="head">Bob Computes</th>
<th class="head">Carol Computes</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>:math:`e(B_{1}^{pk}, C_{2}^{pk})^{A^{sk}}`</td>
<td>:math:`e(C_{1}^{pk}, A_{2}^{pk})^{B^{sk}}`</td>
<td>:math:`e(A_{1}^{pk}, B_{2}^{pk})^{C^{sk}}`</td>
</tr>
<tr>
<td colspan="3">All equivalent to :math:`e(g_{1}, g_{2})^{A^{sk} B^{sk} C^{sk}}`</td>
</tr>
</tbody>
</table>
Or, if you prefer code, check out an example from our new library:
<table class="codehilitetable table table-responsive table-borderless">
<tbody>
<tr>
<td class="linenos">
<div class="linenodiv">
<pre> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16</pre>
</div></td>
<td class="code">
<div class="codehilite">
<pre><span class="c1">// Generate private keys</span>
<span class="kd">let</span> <span class="n">alice_sk</span> <span class="o">=</span> <span class="n">Scalar</span>::<span class="n">random</span><span class="p">(</span><span class="n">rng</span><span class="p">);</span>
<span class="kd">let</span> <span class="n">bob_sk</span> <span class="o">=</span> <span class="n">Scalar</span>::<span class="n">random</span><span class="p">(</span><span class="n">rng</span><span class="p">);</span>
<span class="kd">let</span> <span class="n">carol_sk</span> <span class="o">=</span> <span class="n">Scalar</span>::<span class="n">random</span><span class="p">(</span><span class="n">rng</span><span class="p">);</span>

<span class="c1">// Generate public keys in G1 and G2</span>
<span class="kd">let</span> <span class="p">(</span><span class="n">alice_pk1</span><span class="p">,</span> <span class="n">alice_pk2</span><span class="p">)</span> <span class="o">=</span> <span class="p">(</span><span class="n">G1</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">alice_sk</span><span class="p">,</span> <span class="n">G2</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">alice_sk</span><span class="p">);</span>
<span class="kd">let</span> <span class="p">(</span><span class="n">bob_pk1</span><span class="p">,</span> <span class="n">bob_pk2</span><span class="p">)</span> <span class="o">=</span> <span class="p">(</span><span class="n">G1</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">bob_sk</span><span class="p">,</span> <span class="n">G2</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">bob_sk</span><span class="p">);</span>
<span class="kd">let</span> <span class="p">(</span><span class="n">carol_pk1</span><span class="p">,</span> <span class="n">carol_pk2</span><span class="p">)</span> <span class="o">=</span> <span class="p">(</span><span class="n">G1</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">carol_sk</span><span class="p">,</span> <span class="n">G2</span>::<span class="n">one</span><span class="p">()</span> <span class="o">*</span> <span class="o">&amp;</span><span class="n">carol_sk</span><span class="p">);</span>

<span class="c1">// Each party computes the shared secret</span>
<span class="kd">let</span> <span class="n">alice_ss</span> <span class="o">=</span> <span class="n">pairing</span><span class="p">(</span><span class="o">&amp;</span><span class="n">bob_pk1</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">carol_pk2</span><span class="p">)</span> <span class="o">^</span> <span class="o">&amp;</span><span class="n">alice_sk</span><span class="p">;</span>
<span class="kd">let</span> <span class="n">bob_ss</span> <span class="o">=</span> <span class="n">pairing</span><span class="p">(</span><span class="o">&amp;</span><span class="n">carol_pk1</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">alice_pk2</span><span class="p">)</span> <span class="o">^</span> <span class="o">&amp;</span><span class="n">bob_sk</span><span class="p">;</span>
<span class="kd">let</span> <span class="n">carol_ss</span> <span class="o">=</span> <span class="n">pairing</span><span class="p">(</span><span class="o">&amp;</span><span class="n">alice_pk1</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">bob_pk2</span><span class="p">)</span> <span class="o">^</span> <span class="o">&amp;</span><span class="n">carol_sk</span><span class="p">;</span>

<span class="n">assert</span><span class="o">!</span><span class="p">(</span><span class="n">alice_ss</span> <span class="o">==</span> <span class="n">bob_ss</span> <span class="o">&amp;&amp;</span> <span class="n">bob_ss</span> <span class="o">==</span> <span class="n">carol_ss</span><span class="p">);</span>
</pre>
</div></td>
</tr>
</tbody>
</table>
<h2>bn</h2>
The "bn" crate is a <a class="reference external" href="https://www.rust-lang.org/">Rust language</a> library for performing these pairing operations using a cryptographic construction designed by our scientists in <a class="reference external" href="http://eprint.iacr.org/2013/879">[BCGTV14]</a>. It uses a Barreto-Naehrig elliptic curve tuned for use in zkSNARKs. The library is new and incomplete and shouldn't be used in production software, but it is a nice step forward in our goal of making this new kind of cryptography more widely understood and easier to use.

Check out the bn crate <a class="reference external" href="https://github.com/zcash/bn">on github</a> or <a class="reference external" href="https://crates.io/crates/bn">on crates.io</a>! And feel free to join <a class="reference external" href="https://inviteme.z.cash/">our Slack</a> or sign up for <a class="reference external" href="https://z.cash/#launch-notification">email notifications</a> from our team!