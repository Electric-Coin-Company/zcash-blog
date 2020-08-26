---
ID: 4948
post_title: 'Explaining SNARKs Part IV: How to make Blind Evaluation of Polynomials Verifiable'
post_name: snark-explain4
post_date: 2017-04-11 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/snark-explain4/
published: true
tags:
  - cryptography
  - explainers
  - zkSNARKs
categories:
  - Technical
---
<p><a class="reference external" href="/blog/snark-explain3/">&lt;&lt; Part III</a></p>
<p>In this part, we build on Part II and III to develop a protocol for verifiable blind evaluation of polynomials, which we will define shortly. In Part V we'll start to see how such a protocol can be used for constructing SNARKs, so bear with me a little bit longer for the connection to SNARKs :).</p>
<p>Suppose, as in <a href="/blog/snark-explain2/">Part II</a>, that Alice has a polynomial :math:`P` of degree :math:`d` and Bob has a point :math:`s\in\mathbb{F}_p` that he chose randomly. We want to construct a protocol that allows Bob to learn :math:`E(P(s))`, i.e. the hiding of :math:`P` evaluated at :math:`s`, with two additional properties:</p>
<ol>
<li><strong>Blindness</strong>: Alice will <em>not</em> learn :math:`s` (and Bob will not learn :math:`P`).</li>
<li><strong>Verifiability</strong>: The probability that Alice sends a value not of the form :math:`E(P(s))` for :math:`P` of degree :math:`d` that is known to her, but Bob still accepts - is negligible.</li>
</ol>
<p>This is what we call <em>verifiable</em> blind  evaluation of a polynomial. The protocol in Part II gave us the first item but not the second. To get verifiability we need an extended version of the Knowledge of Coefficient Assumption (KCA) that was presented in Part III.</p>
<p>The verifiability and blindness properties are useful together because they make Alice decide what polynomial :math:`P` she will use <em>without seeing</em> :math:`s`. <a class="footnote-reference" href="#id3" id="id1">[1]</a> This, in a sense, commits Alice to an "answer polynomial" without seeing the "challenge point" :math:`s`. This intuition will become more clear in the next parts of the series.</p>
<h2>An Extended KCA</h2>
<p>The KCA as we defined it in Part III essentially said something like this: If Bob gives Alice some :math:`\alpha`-pair :math:`(a,b = \alpha\cdot a)` and then Alice generates another :math:`\alpha`-pair :math:`(a',b')`, then she knows :math:`c` such that :math:`a'=c\cdot a`. In other words, Alice knows the relation between :math:`a'` and :math:`a`.</p>
<p>Now, suppose that instead of one, Bob sends Alice several :math:`\alpha`-pairs :math:`(a_1,b_1),\ldots,(a_d,b_d)` (for the same :math:`\alpha`); and that again, after receiving these pairs, Alice is challenged to generate some other :math:`\alpha`-pair :math:`(a',b')`. Recall that the main point is that Alice must do so although <em>she does not know</em> :math:`\alpha`.</p>
<p>As we saw in Part III, a natural way for Alice to generate such an :math:`\alpha`-pair, would be to take one of the pairs :math:`(a_i,b_i)` she received from Bob, and multiply both elements by some :math:`c\in\mathbb{F}^*_p`; if :math:`(a_i,b_i)` was an :math:`\alpha`-pair, then :math:`(c\cdot a_i,c\cdot b_i)` will be one too. But can Alice generate :math:`\alpha`-pairs in more ways now that she's received <em>multiple</em> :math:`\alpha`-pairs? Perhaps using several of the received :math:`\alpha`-pairs <em>simultaneously</em> to get a new one?</p>
<p>The answer is yes: For example, Alice can choose <em>two</em> values :math:`c_1,c_2\in \mathbb{F}_p` and compute the pair :math:`(a',b')=(c_1\cdot a_1 + c_2\cdot a_2, c_1\cdot b_1 + c_2\cdot b_2)`. An easy computation shows that, as long as :math:`a'` is non-zero, this is also an :math:`\alpha`-pair:</p>
<p>:math:`b' = c_1\cdot b_1 + c_2 \cdot b_2 = c_1 \alpha \cdot a_1 + c_2\alpha\cdot a_2 = \alpha (c_1\cdot a_1 + c_2\cdot a_2) = \alpha\cdot a'.`</p>
<p>More generally, Alice can take any <em>linear combination</em> of the given :math:`d` pairs - that is choose any :math:`c_1,\ldots,c_d\in\mathbb{F}_p` and define :math:`(a',b')=(\sum_{i=1}^d c_i a_i,\sum_{i=1}^d c_ib_i)`.</p>
<p>Note that, if Alice uses this strategy to generate her :math:`\alpha`-pair she will know some linear relation between :math:`a'` and :math:`a_1,\ldots,a_d`; that is, she knows :math:`c_1,\ldots,c_d` such that :math:`a'=\sum_{i=1}^d c_i\cdot a_i`.</p>
<p>The extended KCA states, essentially, that this is the only way Alice can generate an :math:`\alpha`-pair; that is, whenever she succeeds, she will know such a linear relation between :math:`a'` and :math:`a_1,\ldots,a_d`. More formally, suppose that :math:`G` is a group of size :math:`p` with generator :math:`g` written additively as in Part III. The <em>d-power Knowledge of Coefficient Assumption</em> (d-KCA) <a class="footnote-reference" href="#id4" id="id2">[2]</a> in :math:`G` is as follows:</p>
<p><strong>d-KCA</strong>: <em>Suppose Bob chooses random</em> :math:`\alpha\in\mathbb{F}_p^*` <em>and</em> :math:`s\in\mathbb{F}_p`, <em>and sends to Alice the</em> :math:`\alpha`-pairs :math:`(g,\alpha\cdot g), (s\cdot g,\alpha s\cdot g),\ldots,(s^d\cdot g,\alpha s^d\cdot g)`. <em>Suppose that Alice then outputs another</em> :math:`\alpha`-pair :math:`(a',b')`. <em>Then, except with negligible probability, Alice knows</em> :math:`c_0,\ldots,c_d\in\mathbb{F}_p` <em>such that</em> :math:`\sum_{i=0}^d c_i s^i\cdot g = a'`.</p>
<p>Note that in the d-KCA Bob does not send an arbitrary set of :math:`\alpha`-pairs, but one with a certain "polynomial structure". This will be useful in the protocol below.</p>
<h2>The Verifiable Blind Evaluation Protocol</h2>
<p>Assume that our <a href="/blog/snark-explain/">HH</a> is the mapping :math:`E(x)=x\cdot g` for a generator :math:`g` of :math:`G` as above.</p>
<p>For simplicity, we present the protocol for this particular :math:`E`:</p>
<ol>
<li>Bob chooses a random :math:`\alpha\in\mathbb{F}_p^*`, and sends to Alice the hidings :math:`g,s\cdot g,\ldots,s^d\cdot g` (of :math:`1,s,\ldots,s^d`) and also the hidings :math:`\alpha\cdot g,\alpha s \cdot g,\ldots,\alpha s^d\cdot g` (of :math:`\alpha,\alpha s,\ldots,\alpha s^d`).</li>
<li>Alice computes :math:`a=P(s)\cdot g` and :math:`b=\alpha P(s)\cdot g` using the elements sent in the first step, and sends both to Bob.</li>
<li>Bob checks that :math:`b=\alpha \cdot a`, and accepts if and only if this equality holds.</li>
</ol>
<p>First, note that given the coefficients of :math:`P`, :math:`P(s)\cdot g` is a linear combination of :math:`g,s\cdot g,\ldots,s^d\cdot g`; and :math:`\alpha P(s)\cdot g` is a linear combination of  :math:`\alpha\cdot g,\alpha s \cdot g,\ldots,\alpha s^d\cdot g`. Thus, similarly to the protocol of Part II, Alice can indeed compute these values from Bob's messages for a polynomial :math:`P` that she knows.</p>
<p>Second, by the d-KCA if Alice sends :math:`a`, :math:`b` such that :math:`b=\alpha \cdot a` then almost surely she knows :math:`c_0,\ldots,c_d\in\mathbb{F}_p` such that :math:`a=\sum_{i=0}^d c_is^i\cdot g`. In that case, :math:`a=P(s)\cdot g` for the polynomial :math:`P(X)=\sum_{i=0}^d c_i\cdot X^i` known to Alice. In other words, the probability that Bob accepts in Step 3 while at the same time Alice does not know such a :math:`P` is negligible.</p>
<p>To summarize, using the d-KCA we've developed a protocol for verifiable blind evaluation of polynomials. In the next posts, we will see how this building block comes to play in SNARK constructions.</p>
<table class="docutils footnote table table-responsive" frame="void" id="id3" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>In the fully formal proof, things are somewhat more subtle, as Alice <em>does</em> see some information about :math:`s` before deciding on her :math:`P` - for example, 	the hidings of :math:`s,\ldots,s^d`.</td>
</tr>
</tbody>
</table>
<table class="docutils footnote table table-responsive" frame="void" id="id4" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[2]</a></td>
<td>The d-KCA was introduced in a <a class="reference external" href="http://www0.cs.ucl.ac.uk/staff/J.Groth/ShortNIZK.pdf">paper</a> of Jens Groth.</td>
</tr>
</tbody>
</table>
<p><a class="reference external" href="/blog/snark-explain5/">Part V &gt;&gt;</a></p>
