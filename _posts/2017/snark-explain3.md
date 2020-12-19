---
ID: 4947
post_title: 'Explaining SNARKs Part III: The Knowledge of Coefficient Test and Assumption'
post_name: snark-explain3
post_date: 2017-03-28 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/snark-explain3/
published: true
tags:
  - cryptography
  - explainers
  - zkSNARKs
categories:
  - Technical
---
<p><a class="reference external" href="/blog/snark-explain2/">&lt;&lt; Part II</a></p>
<p>In Part II, we saw how Alice can blindly evaluate the hiding :math:`E(P(s))` of her polynomial :math:`P` of degree :math:`d`, at a point :math:`s` belonging to Bob. We called this "blind" evaluation, because Alice did not learn :math:`s` in the process.</p>
<p>However, there was something missing in that protocol - the fact that Alice is <em>able</em> to compute :math:`E(P(s))` does not guarantee she will indeed send :math:`E(P(s))` to Bob, rather than some completely unrelated value.</p>
<p>Thus, we need a way to "force" Alice to follow the protocol correctly. We will explain in part IV precisely how we achieve this. In this post, we focus on explaining the basic tool needed for that - which we call here the <em>Knowledge of Coefficient (KC) Test</em>.</p>
<p>As before, we denote by :math:`g` a generator of a group :math:`G` of order :math:`|G|=p` where the discrete log is hard. It will be convenient from this post onwards to write our group additively rather than multiplicatively. That is, for :math:`\alpha\in\mathbb{F}_p`, :math:`\alpha\cdot g` denotes the result of summing :math:`\alpha` copies of :math:`g`.</p>
<h2>The KC Test</h2>
<p>For :math:`\alpha\in\mathbb{F}_p^*` <a class="footnote-reference" href="#id4" id="id1">[1]</a>, let us call a pair of elements :math:`(a,b)` in :math:`G` an :math:`\alpha`-pair if :math:`a,b \neq 0` and :math:`b=\alpha\cdot a.`</p>
<p>The KC Test proceeds as follows.</p>
<ol>
<li>Bob chooses random :math:`\alpha\in\mathbb{F}_p^*` and :math:`a\in G.` He computes :math:`b=\alpha\cdot a.`</li>
<li>He sends to Alice the "challenge" pair :math:`(a,b).` Note that :math:`(a,b)` is an :math:`\alpha`-pair.</li>
<li>Alice must now respond with a <em>different</em> pair :math:`(a',b')` that is also an :math:`\alpha`-pair.</li>
<li>Bob accepts Alice's response only if :math:`(a',b')` is indeed an :math:`\alpha`-pair. (As he knows :math:`\alpha` he can check if :math:`b'=\alpha\cdot a'.)`</li>
</ol>
<p>Now, let's think how Alice could successfully respond to the challenge. Let's assume for a second that she <em>knew</em> :math:`\alpha.` In that case, she could simply choose any :math:`a'` in :math:`G,` and compute :math:`b'=\alpha\cdot a';` and return :math:`(a',b')` as her new :math:`\alpha`-pair.</p>
<p>However, as the only information about :math:`\alpha` she has is :math:`\alpha\cdot a` and :math:`G` has a hard discrete log problem, we expect that Alice cannot find :math:`\alpha.`</p>
<p>So how can she successfully respond to the challenge without knowing :math:`\alpha?`</p>
<p>Here's the natural way to do it: Alice simply chooses some :math:`\gamma\in\mathbb{F}_p^*,` and responds with :math:`(a',b')=(\gamma\cdot a,\gamma\cdot b).`</p>
<p>In this case, we have:</p>
<p>:math:`b'=\gamma \cdot b = \gamma \alpha \cdot a = \alpha (\gamma\cdot a) =\alpha \cdot a',`</p>
<p>so indeed :math:`(a',b')` is an :math:`\alpha`-pair as required.</p>
<p>Note that if Alice responds using this strategy, she <em>knows the ratio</em> between :math:`a` and :math:`a'`. That is, she knows the coefficient :math:`\gamma` such that :math:`a'=\gamma\cdot a.`</p>
<p>The Knowledge of Coefficient Assumption <a class="footnote-reference" href="#id5" id="id2">[2]</a> (KCA) states that <em>this is always the case</em>, namely:</p>
<p><em>KCA: If Alice returns a valid response</em> :math:`(a',b')` <em>to Bob's challenge</em> :math:`(a,b)` <em>with non-negligible probability over Bob's choices of</em> :math:`a,\alpha`, <em>then she knows</em> :math:`\gamma` <em>such that</em> :math:`a'=\gamma\cdot a.`</p>
<p>The KC Test and Assumption will be important tools in Part IV.</p>
<h2>What does "Alice knows" mean exactly</h2>
<p>You may wonder how we can phrase the KCA in precise mathematical terms; specifically, how do we formalize the notion that "Alice knows :math:`\gamma`" in a mathematical definition?</p>
<p>This is done roughly as follows: We say that, in addition to Alice, we have another party which we call <em>Alice's Extractor</em>. Alice's Extractor has access to Alice's inner state.</p>
<p>We then formulate the KCA as saying that: whenever Alice successfully responds with an :math:`\alpha`-pair :math:`(a',b'),` Alice's Extractor outputs :math:`\gamma` such that :math:`a'=\gamma\cdot a.` <a class="footnote-reference" href="#id6" id="id3">[3]</a></p>
<table class="docutils footnote table table-responsive" frame="void" id="id4" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>:math:`\mathbb{F}_p^*` denotes the non-zero elements of :math:`\mathbb{F}_p`. It is the same as :math:`\mathbb{Z}_p^*` described in Part I.</td>
</tr>
</tbody>
</table>
<table class="docutils footnote table table-responsive" frame="void" id="id5" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[2]</a></td>
<td>This is typically called the Knowledge of Exponent Assumption in the literature, as traditionally it was used for groups written multiplicatively.</td>
</tr>
</tbody>
</table>
<table class="docutils footnote table table-responsive" frame="void" id="id6" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id3">[3]</a></td>
<td>The fully formal definition needs to give the Extractor "a little slack" and states instead that the probability that Alice responds successfully but the Extractor does not output such :math:`\gamma` is negligible.</td>
</tr>
</tbody>
</table>
<p><a class="reference external" href="/blog/snark-explain4.html">Part IV &gt;&gt;</a></p>
