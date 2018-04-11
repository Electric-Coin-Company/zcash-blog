---
ID: 1625
post_title: 'Explaining SNARKs Part II: Blind Evaluation of Polynomials'
author: Ariel Gabizon
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/snark-explain2/
published: true
post_date: 2017-03-13 00:00:00
---
<a class="reference external" href="/snark-explain/">&lt;&lt; Part I</a>

In this post, we recall the notion of a polynomial, and explain the notion of "blind evaluation" of a polynomial, and how it is implemented using Homomorphic Hiding (HH). (See <a class="reference external" href="/snark-explain/">Part I</a> for an explanation of HH. ) In future posts, we will see that blind evaluation is a central tool in SNARK constructions.

We denote by :math:`\mathbb{F}_p` the field of size :math:`p`; that is, the elements of :math:`\mathbb{F}_p` are :math:`\{0,\ldots,p-1\}` and addition and multiplication are done :math:`\mathrm{mod}\;p` as explained in Part I.
<h2>Polynomials and linear combinations</h2>
Recall that a polynomial :math:`P` of degree :math:`d` over :math:`\mathbb{F}_p` is an expression of the form

:math:`P(X) = a_0 + a_1\cdot X + a_2\cdot X^2 + \ldots + a_d\cdot X^d`

, for some :math:`a_0,\ldots,a_d\in\mathbb{F}_p.`

We can <em>evaluate</em> :math:`P` at a point :math:`s\in {\mathbb{F}_p}` by substituting :math:`s` for :math:`X`, and computing the resultant sum

:math:`P(s) = a_0 + a_1\cdot s + a_2\cdot s^2 + \ldots + a_d\cdot s^d`

For someone that knows :math:`P,` the value :math:`P(s)` is a <em>linear combination</em> of the values :math:`1,s,\ldots,s^d` - where linear combination just means "weighted sum", in the case of :math:`P(s)` the "weights" are :math:`a_0,\ldots,a_d.`

In the last post, we saw the HH :math:`E` defined by :math:`E(x)=g^x` where :math:`g` was a generator of a group with a hard discrete log problem. We mentioned that this HH "supports addition" in the sense that :math:`E(x+y)` can be computed from :math:`E(x)` and :math:`E(y)`. We note here that it also "supports linear combinations"; meaning that, given :math:`a,b,E(x),E(y),` we can compute :math:`E(ax+by)`. This is simply because

:math:`E(ax+by)=g^{ax+by}=g^{ax}\cdot g^{by} = (g^x)^a\cdot (g^y)^b = E(x)^a\cdot E(y)^b.`
<h2>Blind evaluation of a polynomial</h2>
Suppose Alice has a polynomial :math:`P` of degree :math:`d`, and Bob has a point :math:`s\in\mathbb{F}_p` that he chose randomly. Bob wishes to learn :math:`E(P(s))`, i.e., the HH of the evaluation of :math:`P` at :math:`s.` Two simple ways to do this are:
<ul>
 	<li>Alice sends :math:`P` to Bob, and he computes :math:`E(P(s))` by himself.</li>
 	<li>Bob sends :math:`s` to Alice; she computes :math:`E(P(s))` and sends it to Bob.</li>
</ul>
However, in the <em>blind evaluation problem</em> we want Bob to learn :math:`E(P(s))` without learning :math:`P` - which precludes the first option; and, most importantly, we don't want Alice to learn :math:`s`, which rules out the second <a class="footnote-reference" href="#id4" id="id2">[1]</a>.

Using HH, we can perform blind evaluation as follows.
<ol>
 	<li>Bob sends to Alice the hidings :math:`E(1),E(s),\ldots,E(s^d).`</li>
 	<li>Alice computes :math:`E(P(s))` from the elements sent in the first step, and sends :math:`E(P(s))` to Bob. (Alice can do this since :math:`E` supports linear combinations, and :math:`P(s)` is a linear combination of :math:`1,s,\ldots,s^d.)`</li>
</ol>
Note that, as only hidings were sent, neither Alice learned :math:`s` <a class="footnote-reference" href="#id5" id="id3">[2]</a>, nor Bob learned :math:`P`.
<h2>Why is this useful?</h2>
Subsequent posts will go into more detail as to how blind evaluation is used in SNARKs. The rough intuition is that the verifier has a "correct" polynomial in mind, and wishes to check the prover knows it. Making the prover blindly evaluate their polynomial at a random point not known to them, ensures the prover will give the wrong answer with high probability if their polynomial is not the correct one. This, in turn, relies on the Schwartz-Zippel Lemma stating that "different polynomials are different at most points".
<table id="id4" class="docutils footnote" frame="void" rules="none">
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[1]</a></td>
<td>The main reason we don't want to send :math:`P` to Bob, is simply that it is large - (d+1) elements, where, for example, d~2000000 in the current Zcash protocol; this ultimately has to do with the "Succinct" part of SNARKs. It is true that the sequence of hidings Bob is sending to Alice above is just as long, but it will turn out this sequence can be "hard-coded" in the parameters of the system, whereas Alice's message will be different for each SNARK proof.</td>
</tr>
</tbody>
</table>
<table id="id5" class="docutils footnote" frame="void" rules="none"><colgroup> <col class="label" /> <col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id3">[2]</a></td>
<td>Actually, the hiding property only guarantees :math:`s` not being recoverable from :math:`E(s)`, but here we want to claim it is also not recoverable from the sequence :math:`E(s),\ldots,E(s^d)` that potentially contains more information about :math:`s`. This follows from the d-power Diffie-Hellman assumption, which is needed in several SNARK security proofs.</td>
</tr>
</tbody>
</table>
<a class="reference external" href="/snark-explain3/">Part III &gt;&gt;</a>