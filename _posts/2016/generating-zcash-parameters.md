---
ID: 4887
post_title: >
  Zcash Parameters And How They Will Be
  Generated
post_name: generating-zcash-parameters
post_date: 2016-09-25 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/generating-zcash-parameters/
published: true
tags:
  - cryptography
  - Parameter Generation
  - zkSNARKs
categories:
  - Technical
---
<p>At its core, Zcash's privacy technology relies on a novel cryptographic tool called a zkSNARK - a small <a href="https://en.wikipedia.org/wiki/Zero-knowledge_proof">zero-knowledge proof</a> that is cheap to verify. Zcash will be the first to employ this powerful tool on a large scale. For these zkSNARKs to work, a setup phase is required where the "system parameters" are generated. This setup phase is similar to the setup phase of a public-key cryptosystem, but with a catch: As in the public-key cryptosystem, a pair (:math:`\mathsf{privkey},` :math:`\mathsf{pubkey)}` is generated, but then :math:`\mathsf{privkey}` is <em>destroyed</em>. Indeed, it will be essential for the integrity of the system that after the setup phase <em>nobody</em> possesses :math:`\mathsf{privkey}.`</p>
<p>:math:`\mathsf{pubkey}` corresponds to the required system parameters. :math:`\mathsf{privkey}` corresponds to what has been called the "toxic waste" <a href="/blog/snark-parameters/">here</a>, and possessing it enables counterfeiting new coins (but does not enable violating the privacy of other users' transactions).</p>
<p>To reduce risk, Zcash has designed a multi-player protocol where :math:`\mathsf{pubkey}` will be generated. The protocol has the property that :math:`\mathsf{privkey}` now corresponds to the concatenation of all participants' secret randomness. Thus, :math:`\mathsf{privkey}` will be destroyed unless <em>all</em> of the participants are dishonest or compromised.</p>
<p>The purpose of this post is to give a simplified explanation of what :math:`\mathsf{pubkey}` looks like, and how the protocol for generating it works.</p>
<h2>What :math:`\mathsf{pubkey}` looks like</h2>
<p>Suppose :math:`g` is a generator of a group :math:`G` where the discrete log is hard. We assume :math:`G` has order :math:`r` for some prime :math:`r,` and we write group operations additively. So for :math:`s\in \mathbb{F}`, where :math:`\mathbb{F}` is the field of size :math:`r`, we can write :math:`s\cdot g` to denote scalar multiplication of :math:`g` by :math:`s`; i.e. :math:`s\cdot g` is obtained by adding :math:`s` copies of :math:`g`. A simplified version of (:math:`\mathsf{privkey},` :math:`\mathsf{pubkey)}` is that :math:`\mathsf{privkey}` is simply a uniformly random element :math:`s\in \mathbb{F}^*` and :math:`\mathsf{pubkey}` is the sequence of group elements</p>
<blockquote><p>:math:`\mathsf{pubkey}=` :math:`(g,s\cdot g, s^2\cdot g,\ldots, s^d\cdot g)`</p></blockquote>
<p>Above, :math:`\mathbb{F}^*` denotes the set of all non-zero elements of :math:`\mathbb{F}.`</p>
<h2>How :math:`\mathsf{pubkey}` is generated</h2>
<p>We'll say a few words later about <em>why</em> :math:`\mathsf{pubkey}` looks like this and how it is used, but let's concentrate for now on designing the protocol for generating :math:`\mathsf{pubkey}.`</p>
<p>Let's fix :math:`d=2` for simplicity; and also omit the first :math:`g` element from :math:`\mathsf{pubkey}`, as it's straightforward to generate that. Suppose we have two parties, Alice and Bob, that wish to generate a valid public key :math:`\mathsf{pubkey}=` :math:`(s\cdot g, s^2\cdot g)` for the system. They wish to do so in a way that will ensure neither of them will know :math:`s.` Let's make it simpler first: suppose they just want to generate :math:`s\cdot g` (again, in a way that neither will know :math:`s)`. They use the following protocol:</p>
<ol>
<li>Alice chooses a random :math:`a\in \mathbb{F}^*`, and sends :math:`M_1:= a\cdot g` to Bob.</li>
<li>Bob then chooses a random :math:`b\in \mathbb{F}^*` and multiplies :math:`M_1` by :math:`b`. He sends back the message :math:`M:= b\cdot M_1` as their joint output.</li>
</ol>
<p>At the end of the protocol, we have :math:`M=b\cdot a \cdot g = (a b)\cdot g`. Let's denote :math:`s:= a b`.</p>
<p>Note that</p>
<ul>
<li>Bob does not learn :math:`a` from the message :math:`M_1,` as we are assuming the discrete log is hard in :math:`G`. Same for Alice and :math:`b.` In particular, neither knows :math:`s` which is the product of :math:`a` and :math:`b`.</li>
<li>For any fixed :math:`a\in \mathbb{F}^*`, :math:`a b` is a random element of :math:`\mathbb{F}^*` when :math:`b` is random. So even if Alice cheats in the sense that she didn't choose :math:`a` randomly as she was supposed to, e.g. she always chooses :math:`a=4`, :math:`s` will be random. Same is true for Bob cheating and not choosing a random :math:`b.`</li>
</ul>
<p>So as long as <em>one of them</em> follows the protocol correctly, :math:`M=s\cdot g` will be of the right form.</p>
<p>Now let's try to use a similar idea for generating :math:`(s\cdot g, s^2\cdot g)`:</p>
<ul>
<li>Alice chooses a random :math:`a\in \mathbb{F}^*,` and sends :math:`(A,B)` where :math:`A:= a\cdot g` and :math:`B := a^2\cdot g.`</li>
<li>Bob chooses a random :math:`b\in \mathbb{F}^*,` and sends :math:`M=(b\cdot A, b^2\cdot B).`</li>
</ul>
<p>If Alice and Bob follow the protocol, we get :math:`M= (b a \cdot g, b^2 a^2 \cdot g) = ( a b\cdot g, (a b)^2\cdot g).` So this vector is of the right form for :math:`s:= a b.`</p>
<p>Here's one problem: What if Bob cheats and multiplies :math:`B` by some :math:`c\neq b^2`? So we get :math:`(a b\cdot g, a^2 c \cdot g),` which is not of the form :math:`(s\cdot g, s^2\cdot g)` for any :math:`s.` We need to somehow check that our output vector <em>is</em> of the form :math:`(s\cdot g, s^2\cdot g)` for some :math:`s.` In many groups, this is conjectured not to be efficiently doable - this is what's called the square decisional Diffie-Hellman assumption. However, in our setting we are working with a group that has a <em>bilinear pairing</em>. This is a map :math:`e:G\times G\to G_T,` into a group :math:`G_T` also of order :math:`r` with generator :math:`\mathbf{g},` written multiplicatively, such that</p>
<p>:math:`e(a\cdot g, b\cdot g) = \mathbf{g}^{a b}`</p>
<p>for any :math:`a,b\in\mathbb{F}.` This gives us the following way to check the output :math:`M` has the right form. We simply check if</p>
<p>:math:`e(g,B) = e(A,A).`</p>
<p>Let's see that if nobody cheated, this check will pass. When nobody cheats we have :math:`A=s\cdot g,` and :math:`B=s^2\cdot g.` So</p>
<p>:math:`e(g,B) = e(g,s^2\cdot g) =\mathbf{g}^{s^2}`,</p>
<p>and also</p>
<p>:math:`e(A,A) = e(s\cdot g,s\cdot g) = \mathbf{g}^{s^2}.`</p>
<p>One can do a similar computation to see that when :math:`M` is not of this form, these two values will differ and the test will fail.</p>
<h2>How :math:`\mathsf{pubkey}` is used</h2>
<p>Recall that a <em>polynomial</em> :math:`P` of degree :math:`d` over :math:`\mathbb{F}` is an expression of the form</p>
<p>:math:`P(X) = a_0 + a_1\cdot X + a_2\cdot X^2 + \ldots + a_d\cdot X^d`</p>
<p>We can <em>evaluate</em> a polynomial at a point :math:`s\in \mathbb{F}` by substituting :math:`s` for :math:`X,` and computing the resultant sum. A useful fact is that if :math:`P` and :math:`Q` are different polynomials of degree at most :math:`d,` they can agree on at most :math:`d` points. In Zcash the sender needs to construct two degree :math:`d` polynomials :math:`P` and :math:`Q` in a certain way, and a lot of mathematical magic ensures that they can make them the same polynomial, i.e., get :math:`P=Q,` only if the transaction is valid.</p>
<p>:math:`\mathsf{pubkey}` can now be used to test if :math:`P` and :math:`Q` are equal at a point :math:`s` <em>not known by the sender</em>. Say</p>
<p>:math:`P(X) = a_0 + a_1\cdot X + a_2\cdot X^2 + \ldots + a_d\cdot X^d`</p>
<p>and</p>
<p>:math:`Q(X) = b_0 + b_1\cdot X + b_2\cdot X^2 + \ldots + b_d\cdot X^d`</p>
<p>Using :math:`\mathsf{pubkey}=` :math:`(g,s\cdot g, s^2\cdot g,\ldots, s^d\cdot g),` the verifier can compute</p>
<p>:math:`P(s)\cdot g = a_0\cdot g + a_1 s \cdot g + a_2s^2 \cdot g + \ldots + a_d s^d\cdot g`</p>
<p>and compute :math:`Q(s)\cdot g` similarly. The verifier can then check if they are equal.</p>
<p>Since the sender of a non-valid transaction has to construct distinct :math:`P` and :math:`Q` without knowing :math:`s,` the chance that :math:`P(s)=Q(s)` is very small.</p>
<h2>Disclaimer</h2>
<p>Please note, this post is a significantly simplified presentation of the underlying protocol. A detailed description can be found in the <a class="reference external" href="https://github.com/zcash/mpc/blob/master/whitepaper.pdf">whitepaper</a>.</p>
<h2>References</h2>
<p>Our zkSNARKS use SCIPR Lab's <a class="reference external" href="https://github.com/scipr-lab/libsnark">implementation</a> of the <a class="reference external" href="https://eprint.iacr.org/2013/279.pdf">Pinnochio protocol</a>, which in turn is based on the <a class="reference external" href="https://eprint.iacr.org/2012/215.pdf">work</a> of Gennaro, Gentry, Parno and Raykova. Our protocol for parameter generation builds on a <a class="reference external" href="http://www.ieee-security.org/TC/SP2015/papers-archived/6949a287.pdf">previous work</a> of Ben-Sasson, Chiesa, Green, Tromer and Virza.</p>
