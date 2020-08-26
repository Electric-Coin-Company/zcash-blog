---
ID: 4945
post_title: 'Explaining SNARKs Part I: Homomorphic Hidings'
post_name: snark-explain
post_date: 2017-02-28 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/snark-explain/
published: true
tags:
  - cryptography
  - explainers
  - zkSNARKs
categories:
  - Technical
---
<p>Constructions of zk-SNARKs involve a careful combination of several ingredients; fully understanding how these ingredients all work together can take a while.</p>
<p>If I had to choose <strong>one ingredient</strong> whose role is most prominent, it would be what I will call here <em>Homomorphic Hiding</em> (HH) <a id="id1" class="footnote-reference" href="#id4">[1]</a>. In this post we explain what an HH is, and then give an example of why it is useful and how it is constructed.</p>
<p>An HH :math:`E(x)` of a number :math:`x` is a function satisfying the following properties:</p>
<ul>
<li>For most :math:`x`'s, given :math:`E(x)` it is hard to find :math:`x.`</li>
<li>Different inputs lead to different outputs - so if :math:`x\neq y,` then :math:`E(x)\neq E(y).`</li>
<li>If someone knows :math:`E(x)` and :math:`E(y),` they can generate the HH of <em>arithmetic expressions in</em> :math:`x` <em>and</em> :math:`y.` For example, they can compute :math:`E(x+y)` from :math:`E(x)` and :math:`E(y).`</li>
</ul>
<p>Here's a toy example of why HH is useful for Zero-Knowledge proofs: Suppose Alice wants to prove to Bob she knows numbers :math:`x,y` such that :math:`x+y=7` (Of course, it's not too exciting knowing such :math:`x,y,` but this is a good example to explain the concept with).</p>
<ol>
<li>Alice sends :math:`E(x)` and :math:`E(y)` to Bob.</li>
<li>Bob computes :math:`E(x+y)` from these values (which he is able to do since :math:`E` is an HH).</li>
<li>Bob also computes :math:`E(7),` and now checks whether :math:`E(x+y)=E(7).` He accepts Alice's proof only if equality holds.</li>
</ol>
<p>As different inputs are mapped by :math:`E` to different hidings, Bob indeed accepts the proof only if Alice sent hidings of :math:`x,y` such that :math:`x+y=7.` On the other hand, Bob does not learn :math:`x` and :math:`y,` as he just has access to their hidings <a id="id2" class="footnote-reference" href="#id5">[2]</a>.</p>
<p>Now let's see an example of how such hidings are constructed. We actually cannot construct them for regular integers with regular addition, but need to look at <em>finite groups</em>:</p>
<p>Let :math:`n` be some integer. When we write :math:`A\;\mathrm{mod}\;n` for an integer :math:`A,` we mean taking the remainder of :math:`A` after dividing by :math:`n.` For example, :math:`9\;\mathrm{mod}\; 7 = 2` and :math:`13\; \mathrm{mod}\;12 = 1.` We can use the :math:`\mathrm{mod}\; n` operation to define an addition operation on the numbers :math:`\{0,\ldots,n-1\}:` We do regular addition but then apply :math:`(\mathrm{mod}\; n)` on the result to get back a number in the range :math:`\{0,\ldots,n-1\}.` We sometimes write :math:`(\mathrm{mod}\; n)` on the right to clarify we are using this type of addition. For example, :math:`2+3 = 1\; (\mathrm{mod} \;4).` We call the set of elements :math:`\{0,\ldots,n-1\}` together with this addition operation the group :math:`\mathbb{Z}_n`.</p>
<p>For a prime :math:`p`, we can use the :math:`\mathrm{mod}\;p` operation to also define a <em>multiplication</em> operation over the numbers :math:`\{1,\ldots,p-1\}` in a way that the multiplication result is also always in the set :math:`\{1,\ldots,p-1\}` - by performing regular multiplication of integers, and then taking the result :math:`\mathrm{mod}\;p.` <a id="id3" class="footnote-reference" href="#id6">[3]</a> For example, :math:`2\cdot 4=1\; (\mathrm{mod}\; 7).`</p>
<p>This set of elements together with this operation is referred to as the group :math:`\mathbb{Z}_p^*`. :math:`\mathbb{Z}_p^*` has the following useful properties:</p>
<ol>
<li>It is a <em>cyclic</em> group; which means that there is some element :math:`g` in :math:`\mathbb{Z}_p^*` called a <em>generator</em> such that all elements of :math:`\mathbb{Z}_p^*` can be written as :math:`g^a` for some :math:`a` in :math:`\{0,..,p-2\}`, where we define :math:`g^0=1.`</li>
<li>The <em>discrete logarithm problem</em> is believed to be hard in :math:`\mathbb{Z}_p^*`. This means that, when p is large, given an element :math:`h` in :math:`\mathbb{Z}_p^*` it is difficult to find the integer :math:`a` in :math:`{0,..,p-2}` such that :math:`g^a=h\;(\mathrm{mod}\;p).`</li>
<li>As ''exponents add up when elements are multiplied'', we have for :math:`a,b` in :math:`{0,..,p-2}` :math:`g^a\cdot g^b = g^{a+b\;(\mathrm{mod}\;p-1)}.`</li>
</ol>
<p>Using these properties, we now construct an HH that ''supports addition'' - meaning that :math:`E(x+y)` is computable from :math:`E(x)` and :math:`E(y).` We assume the input :math:`x` of :math:`E` is from :math:`\mathbb{Z}_{p-1}`, so it is in the range :math:`\{0,\ldots,p-2\}.` We define :math:`E(x)=g^x` for each such :math:`x`, and claim that :math:`E` is an HH: The first property implies that different :math:`x`'s in :math:`\mathbb{Z}_{p-1}` are mapped to different outputs. The second property implies that given :math:`E(x)=g^x` it is hard to find :math:`x`. Finally, using the third property, given :math:`E(x)` and :math:`E(y)` we can compute :math:`E(x+y)` as :math:`E(x+y) = g^{x+y\;\mathrm{mod}\; p-1} = g^x\cdot g^y = E(x)\cdot E(y).`</p>
<table id="id4" class="docutils footnote table table-responsive" frame="void" rules="none">
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>Homomorphic hiding is not a term formally used in cryptography, and is introduced here for didactic purposes. It is similar to but weaker than the well-known notion of a computationally hiding commitment. The difference is that an HH is a deterministic function of the input, whereas a commitment uses additional randomness. As a consequence, HHs essentially ''hide most x's'' whereas commitments ''hide every x''.</td>
</tr>
</tbody>
</table>
<table id="id5" class="docutils footnote table table-responsive" frame="void" rules="none">
<colgroup>
<col class="label"> </colgroup>
<colgroup>
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[2]</a></td>
<td>Bob does learn <em>some</em> information about x and y. For example, he can choose a random x', and check whether x=x' by computing E(x'). For this reason the above protocol is not really a Zero-Knowledge protocol, and is only used here for explanatory purposes. In fact, as we shall see in later posts, HH is ultimately used in snarks to conceal verifier challenges rather than prover secrets.</td>
</tr>
</tbody>
</table>
<table id="id6" class="docutils footnote table table-responsive" frame="void" rules="none">
<colgroup>
<col class="label"> </colgroup>
<colgroup>
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id3">[3]</a></td>
<td>When p is not a prime it is problematic to define multiplication this way. One issue is that the multiplication result can be zero even when both arguments are not zero. For example when p=4, we can get 2*2=0 (mod 4).</td>
</tr>
</tbody>
</table>
<p><a class="reference external" href="/blog/snark-explain2">Part II &gt;&gt;</a></p>
