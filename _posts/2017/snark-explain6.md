---
ID: 4950
post_title: 'Explaining SNARKs Part VI: The Pinocchio Protocol'
post_name: snark-explain6
post_date: 2017-05-10 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/snark-explain6/
published: true
tags:
  - cryptography
  - explainers
  - zkSNARKs
categories:
  - Technical
---
<p><a class="reference external" href="/blog/snark-explain5/">&lt;&lt; Part V</a></p>
<p>In part V we saw how a statement Alice would like to prove to Bob can be converted into an equivalent form in the "language of polynomials" called a Quadratic Arithmetic Program (QAP).</p>
<p>In this part, we show how Alice can send a very short proof to Bob showing she has a satisfying assignment to a QAP. We will use the <a class="reference external" href="https://eprint.iacr.org/2013/279.pdf">Pinocchio Protocol</a> of Parno, Howell, Gentry and Raykova. But first let us recall the definition of a QAP we gave last time:</p>
<p><em>A Quadratic Arithmetic Program</em> :math:`Q` <em>of degree</em> :math:`d` <em>and size</em> :math:`m` <em>consists of polynomials</em> :math:`L_1,\ldots,L_m`, :math:`R_1,\ldots,R_m`, :math:`O_1,\ldots,O_m` <em>and a target polynomial</em> :math:`T` <em>of degree</em> :math:`d`.</p>
<p><em>An assignment</em> :math:`(c_1,\ldots,c_m)` <strong>satisfies</strong> :math:`Q` <em>if, defining</em><br />
:math:`L:=\sum_{i=1}^m c_i\cdot L_i, R:=\sum_{i=1}^m c_i\cdot R_i, O:=\sum_{i=1}^m c_i\cdot O_i` <em>and</em> :math:`P:=L\cdot R -O`, <em>we have that</em> :math:`T` <em>divides</em> :math:`P`.</p>
<p>As we saw in Part V, Alice will typically want to prove she has a satisfying assignment possessing some additional constraints, e.g. :math:`c_m=7`; but we ignore this here for simplicity, and show how to just prove knowledge of <em>some</em> satisfying assignment.</p>
<p>If Alice has a satisfying assignment it means that, defining :math:`L,R,O,P` as above, there exists a polynomial :math:`H` such that :math:`P=H\cdot T`. In particular, for any :math:`s\in\mathbb{F}_p` we have :math:`P(s)=H(s)\cdot T(s)`.</p>
<p>Suppose now that Alice <em>doesn't</em> have a satisfying assignment, but she still constructs :math:`L,R,O,P` as above from some unsatisfying assignment :math:`(c_1,\ldots,c_m)`. Then we are guaranteed that :math:`T` does not divide :math:`P`. This means that for any polynomial :math:`H` of degree at most :math:`d-2`, :math:`P` and :math:`L,R,O,H` will be different polynomials. Note that :math:`P` here is of degree at most :math:`2(d-1)`, :math:`L,R,O` here are of degree at most :math:`d-1` and :math:`H` here is degree at most :math:`d-2`.</p>
<p>Now we can use the famous <a href="https://en.wikipedia.org/wiki/Schwartz%E2%80%93Zippel_lemma">Schwartz-Zippel Lemma</a> that tells us that two different polynomials of degree at most :math:`2d` can agree on at most :math:`2d` points :math:`s\in\mathbb{F}_p`. Thus, if :math:`p` is much larger than :math:`2d` the probability that :math:`P(s)=H(s)\cdot T(s)` for a randomly chosen :math:`s\in\mathbb{F}_p` is very small.</p>
<p>This suggests the following protocol sketch to test whether Alice has a satisfying assignment.</p>
<ol>
<li>Alice chooses polynomials :math:`L,R,O,H` of degree at most :math:`d`.</li>
<li>Bob chooses a random point :math:`s\in\mathbb{F}_p`, and computes :math:`E(T(s))`.</li>
<li>Alice sends Bob the <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/snark-explain/">hidings</a> of all these polynomials evaluated at :math:`s`, i.e. :math:`E(L(s)),E(R(s)),E(O(s)),E(H(s))`.</li>
<li>Bob checks if the desired equation holds at :math:`s`. That is, he checks whether :math:`E(L(s)\cdot R(s)-O(s))=E(T(s)\cdot H(s))`.</li>
</ol>
<p>Again, the point is that if Alice does not have a satisfying assignment, she will end up using polynomials where the equation does not hold identically, and thus does not hold at most choices of :math:`s`. Therefore, Bob will reject with high probability over his choice of :math:`s` in such a case.</p>
<p>The question is whether we have the tools to implement this sketch. The most crucial point is that Alice must choose the polynomials she will use, <em>without</em> knowing :math:`s`. But this is exactly the problem we solved in the <a href="/blog/snark-explain4/">verifiable blind evaluation protocol</a>, that was developed in Parts II-IV.</p>
<p>Given that we have that, there are four main points that need to be addressed to turn this sketch into a zk-SNARK. We deal with two of them here, and the other two in the next part.</p>
<h2>Making sure Alice chooses her polynomials according to an assignment</h2>
<p>Here is an important point: If Alice doesn't have a satisfying assignment, it doesn't mean she can't find <em>any</em> polynomials :math:`L,R,O,H` of degree at most :math:`d` with :math:`L\cdot R-O=T\cdot H`, it just means she can't find such polynomials where :math:`L,R` and :math:`O` were "produced from an assignment"; namely, that :math:`L:=\sum_{i=1}^m c_i\cdot L_i, R:=\sum_{i=1}^m c_i\cdot R_i, O:=\sum_{i=1}^m c_i\cdot O_i` for <em>the same</em> :math:`(c_1,\ldots,c_m)`.</p>
<p>The protocol of Part IV just guarantees she is using some polynomials :math:`L,R,O` of the right degree, but not that they were produced from an assignment. This is a point where the formal proof gets a little subtle; here we sketch the solution imprecisely.</p>
<p>Let's combine the polynomials :math:`L,R,O` into one polynomial :math:`F` as follows:</p>
<p>:math:`F=L+X^{d+1}\cdot R+X^{2(d+1)}\cdot O`</p>
<p>The point of multiplying :math:`R` by :math:`X^{d+1}` and :math:`O` by :math:`X^{2(d+1)}` is that the coefficients of :math:`L,R,O` "do not mix" in :math:`F`: The coefficients of :math:`1,X,\ldots,X^d` in :math:`F` are precisely the coefficients of :math:`L`, the next :math:`d+1` coefficients of :math:`X^{d+1},\ldots,X^{2d+1}` are precisely the coefficients of :math:`R`, and the last :math:`d+1` coefficients are those of :math:`O`.</p>
<p>Let's combine the polynomials in the QAP definition in a similar way, defining for each :math:`i\in \{1,\ldots,m\}` a polynomial :math:`F_i` whose first :math:`d+1` coefficients are the coefficients of :math:`L_i`, followed be the coefficients of :math:`R_i` and then :math:`O_i`. That is, for each :math:`i\in \{1,\ldots,m\}` we define the polynomial</p>
<p>:math:`F_i=L_i+X^{d+1}\cdot R_i+X^{2(d+1)}\cdot O_i`</p>
<p>Note that when we sum two of the :math:`F_i`'s the :math:`L_i`, :math:`R_i`, and :math:`O_i` "sum separately". For example, :math:`F_1+F_2 = (L_1+L_2)+X^{d+1}\cdot (R_1+R_2)+X^{2(d+1)}\cdot(O_1+O_2)`.</p>
<p>More generally, suppose that we had :math:`F=\sum_{i=1}^mc_i\cdot F_i` for some :math:`(c_1,\ldots,c_m)`. Then we'll also have :math:`L=\sum_{i=1}^m c_i\cdot L_i, R=\sum_{i=1}^m c_i\cdot R_i, O=\sum_{i=1}^m c_i\cdot O_i` for the same coefficients :math:`(c_1,\ldots,c_m)`. In other words, if :math:`F` is a linear combination of the :math:`F_i`'s it means that :math:`L,R,O` were indeed produced from an assignment.</p>
<p>Therefore, Bob will ask Alice to prove to him that :math:`F` is a linear combination of the :math:`F_i`'s. This is done in a similar way to the protocol for verifiable evaluation:</p>
<p>Bob chooses a random :math:`\beta\in\mathbb{F}^*_p`, and sends to Alice the hidings :math:`E(\beta\cdot F_1(s)),\ldots,E(\beta\cdot F_m(s))`. He then asks Alice to send him the element :math:`E(\beta\cdot F(s))`. If she succeeds, an extended version of the <a href="/blog/snark-explain3/">Knowledge of Coefficient Assumption</a> implies she knows how to write :math:`F` as a linear combination of the :math:`F_i`'s.</p>
<h2>Adding the zero-knowledge part - concealing the assignment</h2>
<p>In a zk-SNARK Alice wants to conceal all information about her assignment. However the hidings :math:`E(L(s)),E(R(s)),E(O(s)),E(H(s))` do provide <em>some</em> information about the assignment.</p>
<p>For example, given some other satisfying assignment :math:`(c'_1,\ldots,c'_m)` Bob could compute the corresponding :math:`L',R',O',H'` and hidings :math:`E(L'(s)),E(R'(s)),E(O'(s)),E(H'(s))`. If these come out different from Alice's hidings, he could deduce that :math:`(c'_1,\ldots,c'_m)` is not Alice's assignment.</p>
<p>To avoid such information leakage about her assignment, Alice will conceal her assignment by adding a "random :math:`T`-shift" to each polynomial. That is, she chooses random :math:`\delta_1,\delta_2,\delta_3\in\mathbb{F}^*_p`, and defines :math:`L_z:=L+\delta_1\cdot T,R_z:=R+\delta_2\cdot T,O_z:=O+\delta_3\cdot T`.</p>
<p>Assume :math:`L,R,O` were produced from a satisfying assignment; hence, :math:`L\cdot R-O = T\cdot H` for some polynomial :math:`H`. As we've just added a multiple of :math:`T` everywhere, :math:`T` also divides :math:`L_z\cdot R_z-O_z`. Let's do the calculation to see this:</p>
<p>:math:`L_z\cdot R_z-O_z = (L+\delta_1\cdot T)(R+\delta_2\cdot T) - O-\delta_3\cdot T` :math:`= (L\cdot R-O) + L\cdot \delta_2\cdot T + \delta_1\cdot T\cdot R + \delta_1\delta_2\cdot T^2 - \delta_3\cdot T\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;` :math:`=T\cdot (H+L\cdot \delta_2 + \delta_1\cdot R + \delta_1 \delta_2\cdot T - \delta_3)`</p>
<p>Thus, defining :math:`H_z=H+L\cdot\delta_2 + \delta_1\cdot R + \delta_1\delta_2\cdot T-\delta_3`, we have that :math:`L_z\cdot R_z-O_z=T\cdot H_z`. Therefore, if Alice uses the polynomials :math:`L_z,R_z,O_z,H_z` instead of :math:`L,R,O,H`, Bob will always accept.</p>
<p>On the other hand, these polynomials evaluated at :math:`s\in\mathbb{F}_p` with :math:`T(s)\neq 0` (which is all but :math:`d` :math:`s`'s), reveal no information about the assignment. For example, as :math:`T(s)` is non-zero and :math:`\delta_1` is random, :math:`\delta_1\cdot T(s)` is a random value, and therefore :math:`L_z(s)=L(s)+\delta_1\cdot T(s)` reveals no information about :math:`L(s)` as it is masked by this random value.</p>
<h2>What's left for next time?</h2>
<p>We presented a sketch of the Pinocchio Protocol in which Alice can convince Bob she possesses a satisfying assignment for a QAP, without revealing information about that assignment. There are two main issues that still need to be resolved in order to obtain a zk-SNARK:</p>
<ul>
<li>In the sketch, Bob needs an HH that "supports multiplication". For example, he needs to compute :math:`E(H(s)\cdot T(s))` from :math:`E(H(s))` and :math:`E(T(s))`. However, we have not seen so far an example of an HH that enables this. We have only seen an HH that supports addition and linear combinations.</li>
<li>Throughout this series, we have discussed <em>interactive</em> protocols between Alice and Bob. Our final goal, though, is to enable Alice to send single-message <em>non-interactive proofs</em>, that are <em>publicly verifiable</em> - meaning that anybody seeing this single message proof will be convinced of its validity, not just Bob (who had prior communication with Alice).</li>
</ul>
<p>Both these issues can be resolved by the use of pairings of elliptic curves, which we will discuss in the next and final part.</p>
<p><a class="reference external" href="https://z.cash/blog/snark-explain7.html">&gt;&gt; Part VII</a></p>
