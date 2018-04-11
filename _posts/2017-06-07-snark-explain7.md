---
ID: 1630
post_title: 'Explaining SNARKs Part VII: Pairings of Elliptic Curves'
author: Ariel Gabizon
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/snark-explain7/
published: true
post_date: 2017-06-07 00:00:00
---
<a class="reference external" href="/snark-explain6/">&lt;&lt; Part VI</a>

In Part VI, we saw an outline of the Pinocchio zk-SNARK. We were missing two things - an HH that supports both addition and multiplication that is needed for the verifier's checks, and a transition from an interactive protocol to a non-interactive proof system.

In this post we will see that using elliptic curves we can obtain a limited, but sufficient for our purposes, form of HH that supports multiplication. We will then show that this limited HH also suffices to convert our protocol to the desired non-interactive system.

We begin by introducing elliptic curves and explaining how they give us the necessary HH.

<h2>Elliptic curves and their pairings</h2>

Assume :math:`p` is a prime larger than :math:`3`, and take some :math:`u,v\in\mathbb{F}_p` such that :math:`4u^3+27v^2\neq 0`. We look at the equation 

:math:`Y^2=X^3 +u\cdot X +v`

An elliptic curve :math:`{\mathcal C}` is the of set of points :math:`(x,y)` <a class="footnote-reference" href="#id6" id="id1">[1]</a> that satisfy such an equation. These curves give us an interesting way to construct groups. The group elements will be the points :math:`(x,y)\in \mathbb{F}^2_p` that are on the curve, i.e., that satisfy the equation, together with a special point :math:`{\mathcal O}`, that for technical reasons is sometimes refered to as the "point at infinity", and serves as the identity element, i.e. the zero of the group.

Now the question is how we add two points :math:`P=(x_1,y_1),Q=(x_2,y_2)` to get a third? The addition rule is derived from a somewhat abstract object called the <em>divisor class group</em> of the curve. For our purposes, all you have to know about this divisor class group is that it imposes the following constraint on the definition of addition: The sum of points on any line must be zero, i.e., :math:`{\mathcal O}`.

Let's see how the addition rule is derived from this constraint. Look at a vertical line, defined by an equation of the form :math:`X=c`. Suppose this line intersects the curve at a point :math:`P=(x_1,y_1)`. Because the curve equation is of the form :math:`Y^2=f(X)`, if :math:`(x_1,y_1)` is on the curve, so is the point :math:`Q:=(x_1,-y_1)`. Moreover, since it's a vertical line and the curve equation is of degree two in :math:`Y`, we can be sure these are the only points where the line and curve intersect.
 
<div class="figure align-center">
<img alt="Test |P+Q=O --&gt; P=-Q|" src="http://blog.z.cash/wp-content/uploads/2017/06/ECVertical.png" style="height: 320px;"/>
</div>

Thus, we must have :math:`P+Q={\mathcal O}` which means :math:`P=-Q`; that is, :math:`Q` is the inverse of :math:`P` in the group.

Now let us look at points :math:`P` and :math:`Q` that have a different first coordinate - that is, :math:`x_1\neq x_2`, and see how to add them. We pass a line through :math:`P` and :math:`Q`.

<div class="figure align-center">
<img alt="Test |P+Q+R=0|" src="http://blog.z.cash/wp-content/uploads/2017/06/ECCregular.png" style="height: 320px;"/>
</div>

Since the curve is defined by a degree three polynomial in :math:`X` and already intersects this (non-vertical) line at two points, it is guaranteed to intersect the line at a third point, that we denote :math:`R=(x,y)`, and no other points.

So we must have :math:`P+Q+R={\mathcal O}`, which means :math:`P+Q=-R`; and we know by now that :math:`-R` is obtained from :math:`R` by flipping the second coordinate from :math:`y` to :math:`-y`.

Thus, we have derived the addition rule for our group: Given points :math:`P` and :math:`Q`, pass a line through them, and then take the "mirror" point of the third intersection point of the line as the addition result. <a class="footnote-reference" href="#id7" id="id2">[2]</a>

This group is usually called :math:`{\mathcal C}(\mathbb{F}_p)` - as it consists of points on the curve :math:`{\mathcal C}` with coordinates in :math:`\mathbb{F}_p`; but let's denote it by :math:`G_1` from now on. Assume for simplicity that the number of elements in :math:`G_1` is a prime number :math:`r`, and is different from :math:`p`. This is many times the case, for example in the curve that Zcash is currently using. In this case, any element :math:`g\in G_1` different from :math:`{\mathcal O}` generates :math:`G_1`.

The smallest integer :math:`k` such that :math:`r` divides :math:`p^k-1` is called the <em>embedding degree</em> of the curve. It is conjectured that when :math:`k` is not too small, say, at least :math:`6`, then the discrete logarithm problem in :math:`G_1`, i.e. finding :math:`\alpha` from :math:`g` and :math:`\alpha \cdot g`, is very hard. (In BN curves <a class="footnote-reference" href="#id8" id="id3">[3]</a> currently used by Zcash :math:`k=12`.)

The multiplicative group of :math:`\mathbb{F}_{p^k}` contains a subgroup of order :math:`r` that we denote :math:`G_T`. We can look at curve points with coordinates in :math:`\mathbb{F}_{p^k}` and not just in :math:`\mathbb{F}_p`. Under the same addition rule, these points also form a group together with :math:`{\mathcal O}` called :math:`{\mathcal C}(\mathbb{F}_{p^k})`. Note that :math:`{\mathcal C}(\mathbb{F}_{p^k})` clearly contains :math:`G_1`. Besides :math:`G_1`, :math:`{\mathcal C}(\mathbb{F}_{p^k})` will contain an additional subgroup :math:`G_2` of order :math:`r` (in fact, :math:`r-1` additional subgroups of order :math:`r`).

Fix generators :math:`g\in G_1,h\in G_2`. It turns out that there is an efficient map, called the <em>Tate reduced pairing</em>, taking a pair of elements from :math:`G_1` and :math:`G_2` into an element of :math:`G_T`,

such that

<ol>
<li>:math:`\mathrm{Tate}(g,h)=\mathbf{g}` for a generator :math:`\mathbf{g}` of :math:`G_T`, and</li>
<li>given a pair of elements :math:`a,b \in \mathbb{F}_r`, we have :math:`\mathrm{Tate}(a\cdot g,b\cdot h)=\mathbf{g}^{ab}`.</li>
</ol>

Defining :math:`\mathrm{Tate}` is a bit beyond the scope of this series, and relies on concepts from algebraic geometry, most prominently that  of <em>divisors</em>. Here's a sketch of :math:`\mathrm{Tate}`'s definition: <a class="footnote-reference" href="#id9" id="id4">[4]</a>

For :math:`a\in\mathbb{F}_p`    the polynomial :math:`(X-a)^r` has a zero of multiplicity :math:`r` at the point :math:`a`, and no other zeroes. For a point :math:`P\in G_1`, divisors enable us to prove there exists a function :math:`f_P` from the curve to :math:`\mathbb{F}_p` that also has, in some precise sense, a zero of multiplicity :math:`r` at :math:`P` and no other zeroes. :math:`\mathrm{Tate}(P,Q)` is then defined as :math:`f_P(Q)^{(p^k-1)/r}`.

It may not seem at all clear what this definition has to do with the stated properties, and indeed the proof that :math:`\mathrm{Tate}` has these properties is quite complex.
 
Defining :math:`E_1(x) := x\cdot g, E_2(x):=x\cdot h, E(x):=x\cdot \mathbf{g}`, we get a weak version of an HH that supports both addition and multiplication: :math:`E_1,E_2,E` are HHs that support addition, and given the hidings :math:`E_1(x)`, :math:`E_2(y)` we can compute :math:`E(xy)`. In other words, if we have the ''right'' hidings of :math:`x` and :math:`y` we can get a (different) hiding of :math:`xy`. But for example, if we had hidings of :math:`x,y,z` we couldn't get a hiding of :math:`xyz`.
 
We move on to discussing non-interactive proof systems. We begin by explaining exactly what we mean by 'non-interactive'.

<h2>Non-interactive proofs in the common reference string model</h2>

The strongest and most intuitive notion of a non-interactive proof is probably the following. In order to prove a certain claim, a prover broadcasts a single message to all parties, with no prior communication of any kind; and anyone reading this message would be convinced of the prover's claim. This can be shown to be impossible in most cases. <a class="footnote-reference" href="#id10" id="id5">[5]</a>

A slightly relaxed notion of non-interactive proof is to allow a common reference string (CRS). In the CRS model, before any proofs are constructed, there is a setup phase where a string is constructed according to a certain randomized process and broadcast to all parties. This string is called the CRS and is then used to help construct and verify proofs. The assumption is that the randomness used in the creation of the CRS is not known to any party - as knowledge of this randomness might enable constructing proofs of false claims.

We will explain how in the CRS model we can convert the verifiable blind evaluation protocol of <a href="/snark-explain4/">Part IV </a> into a non-interactive proof system. As the protocol of Part VI consisted of a few such subprotocols it can be turned into a non-interactive proof system in a similar way.

<h2>A non-interactive evaluation protocol</h2>

The non-interactive version of the evaluation protocol basically consists of publishing Bob's first message as the CRS. Recall that the purpose of the protocol is to obtain the hiding :math:`E(P(s))` of Alice's polynomial :math:`P` at a randomly chosen :math:`s\in\mathbb{F}_r`.
  
<strong>Setup</strong>: Random :math:`\alpha\in \mathbb{F}_r^*,s\in\mathbb{F}_r` are chosen and the CRS: 

:math:`(E_1(1),E_1(s),\ldots,E_1(s^d),` :math:`E_2(\alpha),E_2(\alpha s),\ldots,E_2(\alpha s^d))`

is published.

<strong>Proof</strong>: Alice computes :math:`a=E_1(P(s))` and :math:`b=E_2(\alpha P(S))` using the elements of the CRS, and the fact that :math:`E_1` and :math:`E_2` <a href="/snark-explain2/">support linear combinations</a>.

<strong>Verification</strong>: Fix the :math:`x,y\in \mathbb{F}_r` such that :math:`a=E_1(x)` and :math:`b=E_2(y)`. Bob computes :math:`E(\alpha x)=\mathrm{Tate}(E_1(x),E_2(\alpha))` and :math:`E(y)=\mathrm{Tate}(E_1(1),E_2(y))`, and checks that they are equal. (If they are equal it implies :math:`\alpha x =y`.)

As explained in Part IV, Alice can only construct :math:`a,b` that will pass the verification check if :math:`a` is the hiding of :math:`P(s)` for a polynomial :math:`P` of degree :math:`d` known to her. The main difference here is that Bob does not need to know :math:`\alpha` for the verification check, as he can use the pairing function to compute :math:`E(\alpha x)` only from :math:`E_1(x)` and :math:`E_2(\alpha)`. Thus, he does not need to construct and send the first message himself, and this message can simply be fixed in the CRS.

<table class="docutils footnote" frame="void" id="id6" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>You may ask 'The set of points from where?'. We mean the set of points with coordinates in the algebraic closure of :math:`\mathbb{F}_p`. Also, the curve has an affine and projective version. When we are referring to the projective version we also include the "point at infinity" :math:`{\mathcal O}` as an element of the curve.</td></tr>
</tbody>
</table>

<table class="docutils footnote" frame="void" id="id7" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label"><a class="fn-backref" href="#id2">[2]</a></td>
<td>We did not address the case of adding :math:`P` to itself. This is done by using the line that is tangent to the curve at :math:`P`, and taking :math:`R` to be the second intersection point of this line with the curve.</td></tr>
</tbody>
</table>

<table class="docutils footnote" frame="void" id="id8" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label"><a class="fn-backref" href="#id3">[3]</a></td><td><a class="reference external" href="https://eprint.iacr.org/2005/133.pdf">https://eprint.iacr.org/2005/133.pdf</a></td></tr>
</tbody>
</table>

<table class="docutils footnote" frame="void" id="id9" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label"><a class="fn-backref" href="#id4">[4]</a></td>
<td>The pairing Zcash actually uses is the <a href="https://www.esat.kuleuven.be/cosic/publications/talk-96.pdf">optimal Ate pairing</a>, which is based on the Tate reduced pairing, and can be computed more efficiently than :math:`\mathrm{Tate}`.</td></tr>
</tbody>
</table>

<table class="docutils footnote" frame="void" id="id10" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label"><a class="fn-backref" href="#id5">[5]</a></td>
<td>In computational complexity theory terms, one can show that only languages in <a href="https://en.wikipedia.org/wiki/BPP_(complexity)">BPP</a> have non-interactive zero-knowledge proofs in this strong sense. The type of claims we need to prove in Zcash transactions, e.g. 'I know a hash preimage of this string', correspond to the complexity class <a href="https://en.wikipedia.org/wiki/NP_(complexity)">NP</a> which is believed to be much larger than BPP. </td></tr>
</tbody>
</table>

<table class="docutils footnote" frame="void" id="id11" rules="none">
<colgroup><col class="label"><col></colgroup>
<tbody valign="top">
<tr><td class="label">[6]</td><td>The images used were taken from the following <a class="reference external" href="https://en.wikipedia.org/wiki/Elliptic_curve">article</a> and are used under the <a class="reference external" href="https://creativecommons.org/licenses/by-sa/3.0/">creative commons license</a>.</td></tr>
</tbody>
</table>