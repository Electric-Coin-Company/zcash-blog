---
ID: 4870
post_title: 'Bellman: zk-SNARKs in Rust'
post_name: bellman-zksnarks-in-rust
post_date: 2017-04-04 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/bellman-zksnarks-in-rust/
published: true
tags:
  - cryptography
  - Rust
  - zkSNARKs
categories:
  - Technical
---
<p><a class="reference external" href="https://github.com/ebfull/bellman">Bellman</a> is a Rust-language library for building zk-SNARKs — small, cheap-to-verify <a class="reference external" href="https://blog.cryptographyengineering.com/2014/11/27/zero-knowledge-proofs-illustrated-primer/">zero-knowledge proofs</a> of arbitrary computations. The goal of bellman is to make it easier for the general public to use and experiment with zk-SNARKs, and also as a step forward for improving the security and performance of Zcash's next major release, <a class="reference external" href="/blog/the-near-future-of-zcash/">Sapling</a>.</p>
<p>Bellman contains an implementation of the <strong>BLS12-381</strong> elliptic curve construction that we <a class="reference external" href="/blog/new-snark-curve/">described</a> a couple weeks ago, which will appear in an upcoming paper by our scientists. This construction was designed specifically for efficiently building zk-SNARKs, while maintaining a high security margin.</p>
<p>This week, I've added a primitive implementation of a <a class="reference external" href="https://eprint.iacr.org/2016/260">new zk-SNARK proving system</a> designed by Jens Groth. Secure in the generic group model, the new design produces smaller proofs that can be constructed faster and with less memory.</p>
<h2>Overview of zk-SNARKs</h2>
<p>If you're interested in how zk-SNARKs work internally, Ariel Gabizon has been writing a <a class="reference external" href="/blog/snark-explain/">series of blog posts</a> about the underlying math that you should check out! For now, we can understand them on a surface level.</p>
<p>zk-SNARKs are powerful proofs that, unlike other zero-knowledge proving schemes, are very small (a couple hundred bytes) and cheap to verify (several milliseconds), even if the statement being proven is large and complicated. Their zero-knowledge property allows the prover to hide details about the computation from the verifier in the process, and so they are useful for both privacy and performance.</p>
<p>The only such schemes known to be efficient are <em>preprocessing</em>. In a sense, this means that a kind of "environment" must be constructed which allows the prover to evaluate the statement and produce a proof. There is no known way to construct such an environment without necessarily being temporarily in possession of information that would allow you to construct false proofs.</p>
<p>Zcash, which uses zk-SNARKs for its shielded transactions, uses parameters that were constructed in a sophisticated multi-party computation ceremony that you can read about <a class="reference external" href="https://z.cash/technology/paramgen.html">here</a>. zk-SNARKs are also useful in the designated verifier model, where the verifier itself constructs the needed parameters, and so neither the prover nor the verifier are concerned about its integrity.</p>
<p>In many zk-SNARK schemes, the statement being proven is reduced to what is called a rank-1 quadratic constraint system, or R1CS. In this system, the prover is given a system of arithmetic constraints over a set of variables (elements in a large prime field :math:`\mathbb{F}_r`), and asked to produce an assignment to the variables which satisfies the constraints.</p>
<h2>Overview of Bellman</h2>
<p>Bellman is currently in its infancy, but we can already use it to construct these kinds of proofs. Currently, only a very low level API is available, upon which we can construct DSLs and various abstractions for synthesizing circuits. If you want to experiment with it, grab the <a class="reference external" href="https://crates.io/crates/bellman">bellman crate from crates.io</a>.</p>
<p>All of our circuit abstractions are written generically over an Engine trait that handles the elliptic curve and finite field arithmetic. Central to circuit synthesis is the ConstraintSystem trait:</p>
<table class="codehilitetable table table-responsive">
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
13</pre>
</div>
</td>
<td class="code">
<div class="codehilite">
<pre><span class="k">pub</span> <span class="k">trait</span> <span class="n">ConstraintSystem</span><span class="o">&lt;</span><span class="n">E</span>: <span class="nc">Engine</span><span class="o">&gt;</span> <span class="p">{</span>
    <span class="sd">/// Allocate a private variable in the constraint system, setting it to</span>
    <span class="sd">/// the provided value.</span>
    <span class="k">fn</span> <span class="nf">alloc</span><span class="p">(</span><span class="o">&amp;</span><span class="k">mut</span> <span class="bp">self</span><span class="p">,</span> <span class="n">value</span>: <span class="nc">E</span>::<span class="n">Fr</span><span class="p">)</span> -&gt; <span class="nc">Variable</span><span class="p">;</span>

    <span class="sd">/// Enforce that `A` * `B` = `C`.</span>
    <span class="k">fn</span> <span class="nf">enforce</span><span class="p">(</span>
        <span class="o">&amp;</span><span class="k">mut</span> <span class="bp">self</span><span class="p">,</span>
        <span class="n">a</span>: <span class="nc">LinearCombination</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span><span class="p">,</span>
        <span class="n">b</span>: <span class="nc">LinearCombination</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span><span class="p">,</span>
        <span class="n">c</span>: <span class="nc">LinearCombination</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span>
    <span class="p">);</span>
<span class="p">}</span>
</pre>
</div>
</td>
</tr>
</tbody>
</table>
<p>There are two important design decisions here:</p>
<ol class="arabic simple">
<li>All variable allocation, assignment, and constraint enforcement is done over the same code path. This differs from the design of libsnark’s gadgetlib, for which it was too easy to potentially forget a constraint or notice bugs in existing abstractions because of the separation. This approach makes it easier to write abstractions and perform code review.</li>
<li>All variable allocation and assignment are done simultaneously, and the existing assignments cannot be queried or modified. This encourages better gadget design, and prevents gadgets from accidentally using the assignments to “communicate” with each other. This also has a performance benefit: since all variables are already assigned, constraint enforcement during proving is directly synthesized into the underlying witnesses to avoid having to keep a constraint system in memory at all.</li>
</ol>
<p>As an example of a kind of gadget implementation, here's how a boolean constrained variable could be implemented, along with XOR:</p>
<table class="codehilitetable table table-responsive">
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
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55</pre>
</div>
</td>
<td class="code">
<div class="codehilite">
<pre><span class="cp">#[derive(Clone)]</span>
<span class="k">pub</span> <span class="k">struct</span> <span class="nc">Bit</span> <span class="p">{</span>
    <span class="n">var</span>: <span class="nc">Variable</span><span class="p">,</span>
    <span class="n">value</span>: <span class="kt">bool</span>
<span class="p">}</span>

<span class="k">impl</span> <span class="n">Bit</span> <span class="p">{</span>
    <span class="k">pub</span> <span class="k">fn</span> <span class="nf">alloc</span><span class="o">&lt;</span><span class="n">E</span><span class="p">,</span> <span class="n">CS</span><span class="o">&gt;</span><span class="p">(</span><span class="n">e</span>: <span class="kp">&amp;</span><span class="nc">E</span><span class="p">,</span>
                        <span class="n">cs</span>: <span class="kp">&amp;</span><span class="nc">mut</span> <span class="n">CS</span><span class="p">,</span>
                        <span class="n">value</span>: <span class="kt">bool</span><span class="p">)</span> -&gt; <span class="nc">Bit</span>
        <span class="k">where</span> <span class="n">E</span>: <span class="nc">Engine</span><span class="p">,</span> <span class="n">CS</span>: <span class="nc">ConstraintSystem</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span> <span class="o">+</span> <span class="o">?</span><span class="nb">Sized</span>
    <span class="p">{</span>
        <span class="c1">// Allocate the variable</span>
        <span class="kd">let</span> <span class="n">var</span> <span class="o">=</span> <span class="n">cs</span><span class="p">.</span><span class="n">alloc</span><span class="p">(</span>
            <span class="k">if</span> <span class="n">value</span> <span class="p">{</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">one</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="p">}</span> <span class="k">else</span> <span class="p">{</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">zero</span><span class="p">()</span> <span class="p">}</span>
        <span class="p">);</span>

        <span class="c1">// Enforce (1 - var) * var = 0, which requires</span>
        <span class="c1">// var to be either 0 or 1</span>
        <span class="n">cs</span><span class="p">.</span><span class="n">enforce</span><span class="p">(</span>
            <span class="n">LinearCombination</span>::<span class="n">one</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="o">-</span> <span class="n">var</span><span class="p">,</span>
            <span class="n">LinearCombination</span>::<span class="n">zero</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="o">+</span> <span class="n">var</span><span class="p">,</span>
            <span class="n">LinearCombination</span>::<span class="n">zero</span><span class="p">(</span><span class="n">e</span><span class="p">)</span>
        <span class="p">);</span>

        <span class="n">Bit</span> <span class="p">{</span>
            <span class="n">var</span>: <span class="nc">var</span><span class="p">,</span>
            <span class="n">value</span>: <span class="nc">value</span>
        <span class="p">}</span>
    <span class="p">}</span>

    <span class="k">pub</span> <span class="k">fn</span> <span class="nf">xor</span><span class="o">&lt;</span><span class="n">E</span><span class="p">,</span> <span class="n">CS</span><span class="o">&gt;</span><span class="p">(</span><span class="o">&amp;</span><span class="bp">self</span><span class="p">,</span>
                      <span class="n">e</span>: <span class="kp">&amp;</span><span class="nc">E</span><span class="p">,</span>
                      <span class="n">cs</span>: <span class="kp">&amp;</span><span class="nc">mut</span> <span class="n">CS</span><span class="p">,</span>
                      <span class="n">other</span>: <span class="kp">&amp;</span><span class="nc">Bit</span><span class="p">)</span> -&gt; <span class="nc">Bit</span>
        <span class="k">where</span> <span class="n">E</span>: <span class="nc">Engine</span><span class="p">,</span> <span class="n">CS</span>: <span class="nc">ConstraintSystem</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span>
    <span class="p">{</span>
        <span class="kd">let</span> <span class="n">new_value</span> <span class="o">=</span> <span class="bp">self</span><span class="p">.</span><span class="n">value</span> <span class="o">^</span> <span class="n">other</span><span class="p">.</span><span class="n">value</span><span class="p">;</span>
        <span class="kd">let</span> <span class="n">new_var</span> <span class="o">=</span> <span class="n">cs</span><span class="p">.</span><span class="n">alloc</span><span class="p">(</span>
            <span class="k">if</span> <span class="n">new_value</span> <span class="p">{</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">one</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="p">}</span> <span class="k">else</span> <span class="p">{</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">zero</span><span class="p">()</span> <span class="p">}</span>
        <span class="p">);</span>

        <span class="c1">// 2a * b = a + b - c</span>
        <span class="n">cs</span><span class="p">.</span><span class="n">enforce</span><span class="p">(</span>
            <span class="n">LinearCombination</span>::<span class="n">zero</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="o">+</span> <span class="bp">self</span><span class="p">.</span><span class="n">var</span> <span class="o">+</span> <span class="bp">self</span><span class="p">.</span><span class="n">var</span><span class="p">,</span>
            <span class="n">LinearCombination</span>::<span class="n">zero</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="o">+</span> <span class="n">other</span><span class="p">.</span><span class="n">var</span><span class="p">,</span>
            <span class="n">LinearCombination</span>::<span class="n">zero</span><span class="p">(</span><span class="n">e</span><span class="p">)</span> <span class="o">+</span> <span class="bp">self</span><span class="p">.</span><span class="n">var</span> <span class="o">+</span> <span class="n">other</span><span class="p">.</span><span class="n">var</span> <span class="o">-</span> <span class="n">new_var</span>
        <span class="p">);</span>

        <span class="n">Bit</span> <span class="p">{</span>
            <span class="n">var</span>: <span class="nc">new_var</span><span class="p">,</span>
            <span class="n">value</span>: <span class="nc">new_value</span>
        <span class="p">}</span>
    <span class="p">}</span>
<span class="p">}</span>
</pre>
</div>
</td>
</tr>
</tbody>
</table>
<p>Building a circuit is a matter of implementing the <cite>Circuit</cite> and <cite>Input</cite> traits:</p>
<table class="codehilitetable table table-responsive">
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
11</pre>
</div>
</td>
<td class="code">
<div class="codehilite">
<pre><span class="k">pub</span> <span class="k">trait</span> <span class="n">Circuit</span><span class="o">&lt;</span><span class="n">E</span>: <span class="nc">Engine</span><span class="o">&gt;</span> <span class="p">{</span>
    <span class="k">type</span> <span class="nc">InputMap</span>: <span class="nc">Input</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;</span><span class="p">;</span>
    <span class="k">fn</span> <span class="nf">synthesize</span><span class="o">&lt;</span><span class="n">CS</span>: <span class="nc">ConstraintSystem</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;&gt;</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span>
                                           <span class="n">engine</span>: <span class="kp">&amp;</span><span class="nc">E</span><span class="p">,</span>
                                           <span class="n">cs</span>: <span class="kp">&amp;</span><span class="nc">mut</span> <span class="n">CS</span><span class="p">)</span>
                                           -&gt; <span class="nc">Self</span>::<span class="n">InputMap</span><span class="p">;</span>
<span class="p">}</span>

<span class="k">pub</span> <span class="k">trait</span> <span class="n">Input</span><span class="o">&lt;</span><span class="n">E</span>: <span class="nc">Engine</span><span class="o">&gt;</span> <span class="p">{</span>
    <span class="k">fn</span> <span class="nf">synthesize</span><span class="o">&lt;</span><span class="n">CS</span>: <span class="nc">PublicConstraintSystem</span><span class="o">&lt;</span><span class="n">E</span><span class="o">&gt;&gt;</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">engine</span>: <span class="kp">&amp;</span><span class="nc">E</span><span class="p">,</span> <span class="n">cs</span>: <span class="kp">&amp;</span><span class="nc">mut</span> <span class="n">CS</span><span class="p">);</span>
<span class="p">}</span>
</pre>
</div>
</td>
</tr>
</tbody>
</table>
<p>This design splits up circuits into a <cite>Circuit</cite> implementation, which provers instantiate to construct proofs, and a <cite>Input</cite> implementation, which provers and verifiers use to perform input allocation and related circuit synthesis. This differs from libsnark, where these code paths are redundant, use different utility functions and require careful code review to ensure consistency.</p>
<p>Once we actually do have an implementation of <cite>Circuit</cite> and <cite>Input</cite>, we can use the functions provided in the <cite>groth16</cite> module: create a keypair (with some randomly selected trapdoors), construct a proof, and perform verifications:</p>
<table class="codehilitetable table table-responsive">
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
16
17
18
19
20
21
22
23
24
25
26
27
28
29</pre>
</div>
</td>
<td class="code">
<div class="codehilite">
<pre><span class="c1">// Create a proving key and verifying key</span>
<span class="kd">let</span> <span class="p">(</span><span class="n">pk</span><span class="p">,</span> <span class="n">vk</span><span class="p">)</span> <span class="o">=</span> <span class="p">{</span>
    <span class="kd">let</span> <span class="n">tau</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">alpha</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">beta</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">gamma</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">delta</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">c</span> <span class="o">=</span> <span class="n">DummyCircuit</span><span class="p">;</span>

    <span class="n">groth16</span>::<span class="n">keypair</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">c</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">tau</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">alpha</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">beta</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">gamma</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">delta</span><span class="p">)</span>
<span class="p">};</span>

<span class="c1">// Construct a proof</span>
<span class="kd">let</span> <span class="n">proof</span> <span class="o">=</span> <span class="p">{</span>
    <span class="kd">let</span> <span class="n">r</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>
    <span class="kd">let</span> <span class="n">s</span> <span class="o">=</span> <span class="n">E</span>::<span class="n">Fr</span>::<span class="n">random</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">rng</span><span class="p">);</span>

    <span class="kd">let</span> <span class="n">c</span> <span class="o">=</span> <span class="n">DummyCircuit</span><span class="p">;</span>

    <span class="n">groth16</span>::<span class="n">prove</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="n">c</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">r</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">s</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">pk</span><span class="p">).</span><span class="n">unwrap</span><span class="p">()</span>
<span class="p">};</span>

<span class="c1">// Prepare the verifying key</span>
<span class="kd">let</span> <span class="n">pvk</span> <span class="o">=</span> <span class="n">groth16</span>::<span class="n">prepare_verifying_key</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">vk</span><span class="p">);</span>

<span class="c1">// Verify proof</span>
<span class="n">assert</span><span class="o">!</span><span class="p">(</span><span class="n">groth16</span>::<span class="n">verify</span><span class="p">(</span><span class="n">e</span><span class="p">,</span> <span class="o">|</span><span class="n">cs</span><span class="o">|</span> <span class="p">{</span>
    <span class="n">DummyInput</span>
<span class="p">},</span> <span class="o">&amp;</span><span class="n">proof</span><span class="p">,</span> <span class="o">&amp;</span><span class="n">pvk</span><span class="p">));</span>
</pre>
</div>
</td>
</tr>
</tbody>
</table>
<h2>Future work</h2>
<p>These lower level foundations are all that is available in Bellman right now. In the future we will be writing tools which allow us to build things like hash functions and stream ciphers.</p>
<p>Bellman is still under development and shouldn’t be used in production software yet. In fact, its API deliberately does not expose anything that would allow you to actually use it! It currently serves as an excellent learning opportunity for constructing zk-SNARKs safely and efficiently, and the lessons we learn from building it will shape the future of Zcash.</p>
<p>We’re also excited to be writing Bellman in Rust! If you’re a Rustacean and you’re interested in zk-SNARKs or Zcash, we invite you to check out <a class="reference external" href="https://github.com/zcash/zcash">our project</a>, join our <a class="reference external" href="https://chat.zcashcommunity.com/">community chat</a> or look at some of the various things we’ve written in Rust before, like our <a class="reference external" href="https://github.com/zcash/mpc">multi-party computation ceremony code</a>.</p>
