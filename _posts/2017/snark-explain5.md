---
ID: 4949
post_title: 'Explaining SNARKs Part V: From Computations to Polynomials'
post_name: snark-explain5
post_date: 2017-04-25 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/snark-explain5/
published: true
tags:
  - cryptography
  - explainers
  - zkSNARKs
categories:
  - Technical
---
<p><a class="reference external" href="/blog/snark-explain4">&lt;&lt; Part IV</a></p>
<p>In the three previous parts, we developed a certain machinery for dealing with polynomials. In this part, we show how to translate statements we would like to prove and verify to the language of polynomials. The idea of using polynomials in this way goes back to the <a class="reference external" href="https://pdfs.semanticscholar.org/4c3a/78661fd920b4116afd0ad88247bbd00160ce.pdf">groundbreaking work</a> of Lund, Fortnow, Karloff and Nisan.</p>
<p>In 2013, <a class="reference external" href="https://eprint.iacr.org/2012/215.pdf">another breakthrough work</a> of Gennaro, Gentry, Parno and Raykova defined an extremely useful translation of computations into polynomials called a <em>Quadratic Arithmetic Program</em> (QAP). QAPs have become the basis for modern zk-SNARK constructions, in particular those used by Zcash.</p>
<p>In this post we explain the translation into QAPs by example. Even when focusing on a small example rather than the general definition, it is unavoidable that it is a lot to digest at first, so be prepared for a certain mental effort :).</p>
<p>Suppose Alice wants to prove to Bob she knows :math:`c_1,c_2,c_3 \in \mathbb{F}_p` such that :math:`(c_1\cdot c_2)\cdot (c_1 + c_3) = 7`. The first step is to present the expression computed from :math:`c_1,c_2,c_3` as an <em>arithmetic circuit</em>.</p>
<h3>Arithmetic circuits</h3>
<p>An arithmetic circuit consists of gates computing arithmetic operations like addition and multiplication, with wires connecting the gates. In our case, the circuit looks like this:</p>

<div class="wp-block-image">
<figure class="aligncenter is-resized"><img src="/wp-content/uploads/2017/04/CircuitDrawing-1.png" alt="" class="wp-image-5322" width="316" height="255"/></figure>
</div>

<p>The bottom wires are the input wires, and the top wire is the output wire giving the result of the circuit computation on the inputs.</p>
<p>As can be seen in the picture, we label the wires and gates of the circuit in a very particular way, that is needed for the next step of translating the circuit into a QAP:
</p>

<ul>
<li>When the same outgoing wire goes into more than one gate, we still think of it as one wire - like :math:`\mathsf{w_1}` in the example.</li>
<li>We assume multiplication gates have exactly two input wires, which we call the left wire and right wire.</li>
<li>We don't label the wires going from an addition to multiplication gate, nor the addition gate; we think of the inputs of the addition gate as going directly into the multiplication gate. So in the example we think of :math:`\mathsf{w_1}` and :math:`\mathsf{w_3}` as both being right inputs of :math:`\mathsf{g_2}`.</li>
</ul>

<p>
A <em>legal assignment</em> for the circuit, is an assignment of values to the labeled wires where the output value of each multiplication gate  is indeed the product of the corresponding inputs.</p>
<p>So for our circuit, a legal assignment is of the form: :math:`(c_1,\ldots,c_5)` where :math:`c_4=c_1\cdot c_2` and :math:`c_5=c_4\cdot (c_1+c_3)`.</p>
<p>In this terminology, what Alice wants to prove is that she knows a legal assignment :math:`(c_1,\ldots,c_5)` such that :math:`c_5=7`. The next step is to translate this statement into one about polynomials using QAPs.
</p>

<h3>Reduction to a QAP</h3>

<p>We associate each multiplication gate with a field element: :math:`\mathsf{g_1}` will be associated with :math:`1\in\mathbb{F}_p` and :math:`\mathsf{g_2}` with :math:`2\in\mathbb{F}_p`. We call the points :math:`\{1,2\}` our <em>target points</em>. Now we need to define a set of "left wire polynomials" :math:`L_1,\ldots,L_5`, "right wire polynomials" :math:`R_1,\ldots,R_5` and "output wire polynomials" :math:`O_1,\ldots,O_5`.</p>
<p>The idea for the definition is that the polynomials will usually be zero on the target points, except the ones involved in the target point's corresponding multiplication gate.</p>
<p>Concretely, as :math:`\mathsf{w_1},\mathsf{w_2},\mathsf{w_4}` are, respectively, the left, right and output wire of :math:`\mathsf{g_1}`; we define :math:`L_1=R_2=O_4=2-X`, as the polynomial :math:`2-X` is one on the point :math:`1` corresponding to :math:`\mathsf{g_1}` and zero on the point :math:`2` corresponding to :math:`\mathsf{g_2}`.</p>
<p>Note that :math:`\mathsf{w_1}` and :math:`\mathsf{w_3}` are <em>both</em> right inputs of :math:`\mathsf{g_2}`. Therefore, we define similarly :math:`L_4=R_1=R_3=O_5=X-1` - as :math:`X-1` is one on the target point :math:`2` corresponding to :math:`\mathsf{g_2}` and zero on the other target point.</p>
<p>We set the rest of the polynomials to be the zero polynomial.</p>
<p>Given fixed values :math:`(c_1,\ldots,c_5)` we use them as coefficients to define a left, right, and output "sum" polynomials. That is, we define</p>
<p>:math:`L:=\sum_{i=1}^5 c_i\cdot L_i, R:=\sum_{i=1}^5 c_i\cdot R_i, O:=\sum_{i=1}^5 c_i\cdot O_i`,</p>
<p>and then we define the polynomia :math:`P:=L\cdot R -O`.</p>
<p>Now, after all these definitions, the central point is this: :math:`(c_1,\ldots,c_5)` <em>is a legal assignment to the circuit if and only if</em> :math:`P` <em>vanishes on all the target points</em>.</p>
<p>Let's examine this using our example. Suppose we defined :math:`L,R,O,P` as above given some :math:`c_1,\ldots,c_5`. Let's evaluate all these polynomials at the target point :math:`1`:</p>
<p>Out of all the :math:`L_i`'s only :math:`L_1` is non-zero on :math:`1`. So we have  :math:`L(1)=c_1\cdot L_1(1)=c_1`. Similarly, we get :math:`R(1)=c_2` and :math:`O(1)=c_4`.</p>
<p>Therefore, :math:`P(1)=c_1\cdot c_2-c_4`. A similar calculation shows :math:`P(2)= c_4\cdot (c_1+c_3) - c_5`.</p>
<p>In other words, :math:`P` vanishes on the target points if and only if :math:`(c_1,\ldots,c_5)` is a legal assignment.</p>
<p>Now, we use the following algebraic fact: For a polynomial :math:`P` and a point :math:`a\in\mathbb{F}_p`, we have :math:`P(a)=0` if and only if the polynomial :math:`X-a` <em>divides</em> :math:`P`, i.e. :math:`P=(X-a)\cdot H` for some polynomial :math:`H`.</p>
<p>Defining the <em>target polynomial</em> :math:`T(X):=(X-1)\cdot (X-2)`, we thus have that :math:`T` divides :math:`P` if and only if :math:`(c_1,\ldots,c_5)` is a legal assignment.</p>
<p>Following the above discussion, we define a QAP as follows:</p>
<p><em>A Quadratic Arithmetic Program</em> :math:`Q` <em>of degree</em> :math:`d` <em>and size</em> :math:`m` <em>consists of polynomials</em> :math:`L_1,\ldots,L_m`, :math:`R_1,\ldots,R_m`, :math:`O_1,\ldots,O_m` <em>and a target polynomial</em> :math:`T` <em>of degree</em> :math:`d`. </p>
<p><em>An assignment</em> :math:`(c_1,\ldots,c_m)` <strong>satisfies</strong> :math:`Q` <em>if, defining</em> :math:`L:=\sum_{i=1}^m c_i\cdot L_i, R:=\sum_{i=1}^m c_i\cdot R_i, O:=\sum_{i=1}^m c_i\cdot O_i` <em>and</em> :math:`P:=L\cdot R -O`, <em>we have that</em> :math:`T` <em>divides</em> :math:`P`.</p>
<p>In this terminology, Alice wants to prove she knows an assignment :math:`(c_1,\ldots,c_5)` satisfying the QAP described above with :math:`c_5=7`.</p>
<p>To summarize, we have seen how a statement such as "I know :math:`c_1,c_2,c_3` such that :math:`(c_1\cdot c_2)\cdot (c_1 + c_3) = 7`" can be translated into an equivalent statement about polynomials using QAPs. In the next part, we will see an efficient protocol for proving knowledge of a satisfying assignment to a QAP.</p>
<p><a class="reference external" href="/blog/snark-explain6">&gt;&gt; Part VI</a></p>
<table class="docutils footnote table table-responsive" frame="void" id="id1" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label">[1]</td>
<td>In this post we tried to give the most concise example of a reduction to QAP; we also recommend Vitalik Buterin's <a href="https://medium.com/@VitalikButerin/quadratic-arithmetic-programs-from-zero-to-hero-f6d558cea649">excellent post</a> for more details on the transformation from a program to a QAP.</td>
</tr>
</tbody>
</table>
