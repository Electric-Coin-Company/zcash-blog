---
ID: 7670
post_title: >
  Lessons From The History Of Attacks On
  Secure Hash Functions
post_name: >
  lessons-from-the-history-of-attacks-on-secure-hash-functions
post_date: 2017-02-24 18:29:48
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/lessons-from-the-history-of-attacks-on-secure-hash-functions/
published: true
tags: [ ]
categories:
  - Technical
---
<p><em>This document is a work-in-progress. Please contact the author if you see errors or omissions.</em></p>
<div class="section" id="summary">
<h2>Summary</h2>
<p>Most of the secure hash functions ever designed have turned out to be vulnerable to collision attacks. This includes the widely-used secure hash functions MD5 and SHA-1.</p>
<p>What about pre-image and second-pre-image attacks? Have practical hash functions historically been vulnerable to those?</p>
<p>I summarize here the history of attacks on secure hash functions in order to yield an answer to that.</p>
<p>The main result is that there is a big gap between the history of collision attacks and pre-image attacks. Almost <em>all</em> older secure hash functions have fallen to collision attacks. Almost <em>none</em> have ever fallen to pre-image attacks.</p>
<p>Secondarily, no <em>new</em> secure hash functions (designed after approximately the year 2000) have so far succumbed to collision attacks, either.</p>
</div>
<div class="section" id="preliminaries">
<h2>Preliminaries</h2>
<p>The input to a secure hash function is called the <em>pre-image</em> and the output is called the <em>image</em>.</p>
<p>A hash function <em>collision</em> is two different inputs (pre-images) which result in the same output. A hash function is <em>collision-resistant</em> if an adversary can't find any collision.</p>
<p>A hash function is <em>pre-image resistant</em> if, given an output (image), an adversary can't find any input (pre-image) which results in that output.</p>
<p>A hash function is <em>second-pre-image resistant</em> if, given <em>one</em> pre-image, an adversary can't find any <em>other</em> pre-image which results in the same image.</p>
</div>
<div class="section" id="when-collision-attacks-don-t-matter">
<h2>When collision attacks don't matter</h2>
<p>There are cases where collision-resistance doesn't matter at all and what you care about is second-pre-image resistance.</p>
<p>For such uses it would be harmless to be able to generate collisions, but harmful to be able to generate pre-images or second-pre-images. For this purpose the relevant question is not whether hash function designs have historically been revealed to be vulnerable to collisions but instead whether they've been revealed to be vulnerable to (second-)pre-images.</p>
<div class="section" id="hash-based-digital-signatures">
<h3>hash-based digital signatures</h3>
<p>An example of this is the construction of hash-based digital signatures. Hash-based digital signatures are secure (resistant to forgery) as long as the hash function they are built on has second-pre-image resistance, e.g. <a class="reference external" href="https://sphincs.cr.yp.to/sphincs-20150202.pdf">SPHINCS</a>.</p>
<p>Such a hash-based digital signature would fail if its underlying hash function failed at second-pre-image resistance, but this is the <em>only</em> way that it could be broken—any attack which was able to forge digital signatures against such a scheme would <em>have</em> to violate the second-pre-image resistance of the underlying hash function.</p>
<p>One reason that hash-based digital signatures might be useful is that if an attacker has a sufficiently large quantum computer, they could forge digital signatures that rely on factorization or discrete log, such as RSA, DSA, ECDSA, or Ed25519. There is no reason to think that such a quantum computer would enable them to break secure hash functions, however.</p>
<p>Another reason is that even if the attacker does <em>not</em> have a sufficiently large quantum computer, but has a mathematical breakthrough that allows them to exploit the asymmetric crypto technique (such as factoring, discrete log, code-based crypto, etc.), then they would be able to exploit asymmetric-crypto-based digital signatures, but not hash-based digital signatures.</p>
<p>What about in the other direction, though? Can't we imagine an attacker who can break hash-based signatures but can't break asymmetric-crypto-based signatures? No—there cannot be such an attacker. Any attacker who can break hash-based signatures can also break asymmetric-crypto-based signatures, because the latter rely on hash functions in addition to relying on their asymmetric crypto primitives.</p>
<p><em>color key: is relying on this safe?</em></p>
<dl class="docutils">
<dt class="r-parent"><span class="r">unsafe</span></dt>
<dd>You can be exploited if you rely on this.</dd>
<dt class="g-parent"><span class="g">safe</span></dt>
<dd>There is no reason to believe that relying on this will make you vulnerable to exploitation.</dd>
</dl>
<p><em>Figure 0: safety of digital signature algorithms</em></p>
<div class="scrollable">
<table class="docutils table table-responsive" border="1">
<colgroup>
<col width="32%">
<col width="8%">
<col width="13%">
<col width="23%">
<col width="12%">
<col width="12%">
</colgroup>
<thead valign="bottom">
<tr>
<th class="head">digital signature type</th>
<th class="head">today</th>
<th class="head">quantum computer</th>
<th class="head">asymmetric crypto breakthrough</th>
<th class="head">hash collisions</th>
<th class="head">hash preimages</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>preimage-resistant-hash-based (<a class="reference external" href="https://sphincs.cr.yp.to/sphincs-20150202.pdf">SPHINCS</a>)</td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
</tr>
<tr>
<td>all other post-quantum (McEliece, NTRUsign, LWE, Ring-LWE, Lattice-based signatures, code-based signatures, Rainbow, multivariate-quadratic, etc.)</td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
</tr>
<tr>
<td>all others (RSA, DSA, ECDSA, Ed25519, etc.)</td>
<td class="g-parent"><span class="g">safe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
<td class="r-parent"><span class="r">unsafe</span></td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
<div class="section" id="when-collision-attacks-do-matter">
<h2>When collision attacks <em>do</em> matter</h2>
<p>Be careful about this! The ability to generate collisions can be surprisingly harmful to many systems. This is one of those subtleties of cryptographic engineering which frequently trip up engineers who are not cryptography experts. The famous “Internet Root Cert” attack <a class="footnote-reference" href="#id120" id="id1">[18]</a> is an example of engineers working at VeriSign incorrectly thinking that their system was not threatened by collisions (in the absence of second-pre-images).</p>
<p><cite>git</cite>, which uses SHA-1, is like VeriSign's MD5 certificates in this way—it is <em>believed</em> by its developers <a class="footnote-reference" href="#id151" id="id2">[50]</a> that a mere collision attack (not second-pre-image) against SHA-1 wouldn't make git users vulnerable to malicious action, but no-one has written a security proof showing that git is safe against this attack.</p>
<p>In contrast to VeriSign and git, the cryptographic constructions mentioned above come with proofs showing that the security of the construction is guaranteed, assuming the security of some underlying component. For example, the hash-based digital signature <a class="reference external" href="https://sphincs.cr.yp.to/sphincs-20150202.pdf">SPHINCS</a> comes with a proof that <em>any possible</em> attack which couldn't generate second-pre-images against the hash function couldn't forge signatures.</p>
</div>
<div class="section" id="results">
<h2>Results</h2>
<p>Here are the results of my search for all state-of-the-art attacks on widely-studied hash functions.</p>
<p><em>The bottom line is that no widely-studied hash function has ever succumbed to a (second-)pre-image attack except for one.</em></p>
<p>That single exception is the second-oldest secure hash function ever designed, <em>Snefru</em>, which was designed in 1989 and 1990, and which turned out to be vulnerable to differential cryptanalysis. Differential cryptanalysis was discovered (by the open research community) in 1990.</p>
<p>No other widely-studied hash function has been shown to be vulnerable to a practical (second-)pre-image attack. Furthermore, no other widely-studied hash function has been shown to be vulnerable to a (second-)pre-image attack that is more efficient than brute force, even if we were to count attacks too expensive for anyone to actually implement!</p>
<p>The history of (second-)pre-image attacks is therefore quite different from the history of collision attacks. Most hash functions have been proven vulnerable to collision attacks more efficient than brute force, and even to collision attacks that could be implemented in practice.</p>
</div>
<div class="section" id="history-of-attacks-on-hash-functions">
<h2>History of attacks on hash functions</h2>
<p>This is a timeline of the publication of hash functions and of publication of weaknesses in hash functions.</p>
<p>I omit attacks on reduced-round or otherwise weakened variants of hash functions (there are a lot of those). I omit attacks that have unrealistic requirements, like attacks that require 2¹²⁸ precomputation or require the messages to be 2⁵⁶ blocks long (there are a lot of those, too).</p>
<p><em>color key: is relying on this safe?</em></p>
<dl class="docutils">
<dt class="r-parent"><span class="r">no</span></dt>
<dd>You can be exploited if you rely on this.</dd>
<dt class="y-parent"><span class="y">maybe</span></dt>
<dd>There are known attacks but they are probably too expensive to actually implement. If the attacks have been secretly improved, or if the attacker has more efficient computational resources than we think, then maybe you can be exploited if you rely on this.</dd>
<dt class="o-parent"><span class="o">maybe</span></dt>
<dd>There are no known attacks that are cheaper than brute force, but the hash output size is small enough that brute force might be feasible, so maybe you can be exploited if you rely on this.</dd>
<dt class="g-parent"><span class="g">yes</span></dt>
<dd>There is no known attack cheaper than brute force, and to pay for a brute force attack is far, far beyond the bounds of possibility for the forseeable future. There is no reason to believe that relying on this will make you vulnerable to exploitation.</dd>
</dl>
<div class="scrollable">
<table class="docutils table table-responsive" border="1">
<caption>Figure 1: Chronological view of collision attacks</caption>
<colgroup>
<col width="5%">
<col width="2%">
<col width="2%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
		</colgroup>
<thead valign="bottom">
<tr>
<th class="head">hash</th>
<th class="head">bits</th>
<th class="head">cpb</th>
<th class="head">'89</th>
<th class="head">'90</th>
<th class="head">'91</th>
<th class="head">'92</th>
<th class="head">'93</th>
<th class="head">'94</th>
<th class="head">'95</th>
<th class="head">'96</th>
<th class="head">'97</th>
<th class="head">'98</th>
<th class="head">'99</th>
<th class="head">'00</th>
<th class="head">'01</th>
<th class="head">'02</th>
<th class="head">'03</th>
<th class="head">'04</th>
<th class="head">'05</th>
<th class="head">'06</th>
<th class="head">'07</th>
<th class="head">'08</th>
<th class="head">'09</th>
<th class="head">'10</th>
<th class="head">'11</th>
<th class="head">'12</th>
<th class="head">'13</th>
<th class="head">'14</th>
<th class="head">'15</th>
<th class="head">'16</th>
<th class="head">'17</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>MD2</td>
<td class="o-parent"><span class="o">&nbsp;</span> 128</td>
<td>638</td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id123" id="id3">[21]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id93" id="id4">[*]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>Snefru-2</td>
<td class="o-parent"><span class="o">&nbsp;</span> 128</td>
<td>?</td>
<td>&nbsp;</td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id105" id="id5">[3]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id121" id="id6">[19]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>MD4</td>
<td class="o-parent"><span class="o">&nbsp;</span> 128</td>
<td>4.0</td>
<td>&nbsp;</td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id124" id="id7">[22]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id122" id="id8">[20]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>RIPEMD</td>
<td class="o-parent"><span class="o">&nbsp;</span> 128</td>
<td>?</td>
<td>&nbsp;</td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id125" id="id9">[23]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id109" id="id10">[7]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>MD5</td>
<td class="o-parent"><span class="o">&nbsp;</span> 128</td>
<td>5.1</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id126" id="id11">[24]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id109" id="id12">[7]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>HAVAL-256-3</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id127" id="id13">[25]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id113" id="id14">[11]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-0</td>
<td class="o-parent"><span class="o">&nbsp;</span> 160</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id128" id="id15">[26]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id95" id="id16">[†]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id129" id="id17">[27]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>GOST</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id130" id="id18">[28]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id116" id="id19">[14]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-1</td>
<td class="o-parent"><span class="o">&nbsp;</span> 160</td>
<td>18</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id131" id="id20">[29]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id117" id="id21">[15]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id152" id="id22">[51]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id154" id="id23">[53]</a></td>
</tr>
<tr>
<td>RIPEMD-160</td>
<td class="o-parent"><span class="o">&nbsp;</span> 160</td>
<td>17</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id132" id="id24">[30]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span> <a class="footnote-reference" href="#id98" id="id25">[‡]</a></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
<td class="o-parent"><span class="o">&nbsp;</span></td>
</tr>
<tr>
<td>Tiger</td>
<td>192</td>
<td>6.2</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id133" id="id26">[31]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Panama</td>
<td>512</td>
<td>2.5</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id135" id="id27">[33]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span> <a class="footnote-reference" href="#id136" id="id28">[34]</a></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="y-parent"><span class="y">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id137" id="id29">[35]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>Whirlpool</td>
<td>512</td>
<td>50</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id134" id="id30">[32]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-256</td>
<td>256</td>
<td>19</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id139" id="id31">[37]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>RadioGatún</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id140" id="id32">[38]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Skein</td>
<td>256</td>
<td>8.7</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id141" id="id33">[39]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Blake</td>
<td>256</td>
<td>17</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id142" id="id34">[40]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Grøstl</td>
<td>256</td>
<td>24</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id143" id="id35">[41]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Keccak (SHA-3)</td>
<td>256</td>
<td>16</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id144" id="id36">[42]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>JH</td>
<td>256</td>
<td>20</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id145" id="id37">[43]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>BLAKE2</td>
<td>256</td>
<td>5.7</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id146" id="id38">[44]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive" border="1">
<caption>Figure 2: Chronological view of (second-)pre-image attacks</caption>
<colgroup>
<col width="5%">
<col width="2%">
<col width="2%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
<col width="3%">
</colgroup>
<thead valign="bottom">
<tr>
<th class="head">hash</th>
<th class="head">bits</th>
<th class="head">cpb</th>
<th class="head">'89</th>
<th class="head">'90</th>
<th class="head">'91</th>
<th class="head">'92</th>
<th class="head">'93</th>
<th class="head">'94</th>
<th class="head">'95</th>
<th class="head">'96</th>
<th class="head">'97</th>
<th class="head">'98</th>
<th class="head">'99</th>
<th class="head">'00</th>
<th class="head">'01</th>
<th class="head">'02</th>
<th class="head">'03</th>
<th class="head">'04</th>
<th class="head">'05</th>
<th class="head">'06</th>
<th class="head">'07</th>
<th class="head">'08</th>
<th class="head">'09</th>
<th class="head">'10</th>
<th class="head">'11</th>
<th class="head">'12</th>
<th class="head">'13</th>
<th class="head">'14</th>
<th class="head">'15</th>
<th class="head">'16</th>
<th class="head">'17</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>MD2</td>
<td class="c-parent"><span class="c">&nbsp;</span> 128</td>
<td>638</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id123" id="id39">[21]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Snefru-2</td>
<td class="c-parent"><span class="c">&nbsp;</span> 128</td>
<td>?</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id105" id="id40">[3]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span> <a class="footnote-reference" href="#id121" id="id41">[19]</a></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
<td class="r-parent"><span class="r">&nbsp;</span></td>
</tr>
<tr>
<td>MD4</td>
<td class="c-parent"><span class="c">&nbsp;</span> 128</td>
<td>4.0</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id124" id="id42">[22]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>RIPEMD</td>
<td class="c-parent"><span class="c">&nbsp;</span> 128</td>
<td>?</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id125" id="id43">[23]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>MD5</td>
<td class="c-parent"><span class="c">&nbsp;</span> 128</td>
<td>5.1</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id126" id="id44">[24]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>HAVAL-256-3</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id127" id="id45">[25]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-0</td>
<td class="c-parent"><span class="c">&nbsp;</span> 160</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id128" id="id46">[26]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>GOST</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id130" id="id47">[28]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-1</td>
<td class="c-parent"><span class="c">&nbsp;</span> 160</td>
<td>18</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id131" id="id48">[29]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>RIPEMD-160</td>
<td class="c-parent"><span class="c">&nbsp;</span> 160</td>
<td>17</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id132" id="id49">[30]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Tiger</td>
<td>192</td>
<td>6.2</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id133" id="id50">[31]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Panama</td>
<td>512</td>
<td>2.5</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id135" id="id51">[33]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Whirlpool</td>
<td>512</td>
<td>50</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id134" id="id52">[32]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>SHA-256</td>
<td>256</td>
<td>19</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id139" id="id53">[37]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>RadioGatún</td>
<td>256</td>
<td>?</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id140" id="id54">[38]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Skein</td>
<td>256</td>
<td>8.7</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id141" id="id55">[39]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Blake</td>
<td>256</td>
<td>17</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id142" id="id56">[40]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Grøstl</td>
<td>256</td>
<td>24</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id143" id="id57">[41]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>Keccak (SHA-3)</td>
<td>256</td>
<td>16</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id144" id="id58">[42]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>JH</td>
<td>256</td>
<td>20</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id145" id="id59">[43]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
<tr>
<td>BLAKE2</td>
<td>256</td>
<td>5.7</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">&nbsp;</span> <a class="footnote-reference" href="#id146" id="id60">[44]</a></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
<td class="g-parent"><span class="g">&nbsp;</span></td>
</tr>
</tbody>
</table>
</div>
<p>I label an attack as cheaper than brute force only if the attack comp times the attack mem is less than the cost of brute force search (see <a class="footnote-reference" href="#id103" id="id61">[1]</a>).</p>
<p>If you are aware of any other papers which fit these criteria, or if you spot an error in this document, please write to me: <a class="reference external" href="mailto:zooko@z.cash">zooko@z.cash</a> .</p>
<p><em>Figure 3: Survey of the best known attacks on secure hash functions</em></p>
<table class="docutils table table-responsive" border="1">
<colgroup>
<col width="22%">
<col width="6%">
<col width="6%">
<col width="5%">
<col width="12%">
<col width="6%">
<col width="5%">
<col width="9%">
<col width="12%">
<col width="6%">
<col width="5%">
<col width="7%">
</colgroup>
<thead valign="bottom">
<tr>
<th class="head" rowspan="2">hash</th>
<th class="head" rowspan="2">year</th>
<th class="head" rowspan="2">bits</th>
<th class="head" rowspan="2">cpb</th>
<th class="head" colspan="4">collision attacks</th>
<th class="head" colspan="4">(second-)preimage attacks</th>
</tr>
<tr>
<th class="head">safe?</th>
<th class="head">comp</th>
<th class="head">mem</th>
<th class="head">ref</th>
<th class="head">safe?</th>
<th class="head">comp</th>
<th class="head">mem</th>
<th class="head">ref</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>MD2</td>
<td>1989</td>
<td>128</td>
<td>638</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2⁶⁴</td>
<td>2⁰</td>
<td><a class="reference internal" href="#id94">[†]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2⁷²</td>
<td>2⁷²</td>
<td><a class="footnote-reference" href="#id104" id="id62">[2]</a></td>
</tr>
<tr>
<td>Snefru -2 <a class="footnote-reference" href="#id105" id="id63">[3]</a></td>
<td>1990</td>
<td>128</td>
<td>?</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2¹³</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id106" id="id64">[4]</a></td>
<td class="r-parent"><span class="r">no</span></td>
<td>2²⁵</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id106" id="id65">[4]</a></td>
</tr>
<tr>
<td>MD4</td>
<td>1990</td>
<td>128</td>
<td>4.0</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2²</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id108" id="id66">[6]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2⁹⁵</td>
<td>2³⁸</td>
<td><a class="footnote-reference" href="#id107" id="id67">[5]</a></td>
</tr>
<tr>
<td>RIPEMD</td>
<td>1990</td>
<td>128</td>
<td>?</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2¹⁸</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id138" id="id68">[36]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>MD5</td>
<td>1992</td>
<td>128</td>
<td>5.1</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2²⁴</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id111" id="id69">[9]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2¹²³</td>
<td>2⁴⁸</td>
<td><a class="footnote-reference" href="#id110" id="id70">[8]</a></td>
</tr>
<tr>
<td>HAVAL-256-3 <a class="footnote-reference" href="#id127" id="id71">[25]</a></td>
<td>1992</td>
<td>256</td>
<td>?</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2²⁹</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id113" id="id72">[11]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2²²⁵</td>
<td>2⁶⁸</td>
<td><a class="footnote-reference" href="#id112" id="id73">[10]</a></td>
</tr>
<tr>
<td>SHA-0</td>
<td>1993</td>
<td>160</td>
<td>?</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2³⁴</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id115" id="id74">[13]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2¹⁸⁹</td>
<td>2⁸</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>GOST</td>
<td>1994</td>
<td>256</td>
<td>?</td>
<td class="y-parent"><span class="y">maybe</span></td>
<td>2¹⁰⁵</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id116" id="id75">[14]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2¹⁹²</td>
<td>2⁷⁰</td>
<td><a class="footnote-reference" href="#id116" id="id76">[14]</a></td>
</tr>
<tr>
<td>SHA-1</td>
<td>1995</td>
<td>160</td>
<td>18</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2⁶³</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id154" id="id77">[53]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>RIPEMD-160 <a class="footnote-reference" href="#id132" id="id78">[30]</a></td>
<td>1996</td>
<td>160</td>
<td>17</td>
<td class="o-parent"><span class="o">maybe</span></td>
<td>2⁸⁰</td>
<td>2⁰</td>
<td><a class="reference internal" href="#id99">[§]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Tiger <a class="footnote-reference" href="#id133" id="id79">[31]</a></td>
<td>1996</td>
<td>192</td>
<td>6.2</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>2¹⁸⁹</td>
<td>2⁸</td>
<td><a class="footnote-reference" href="#id118" id="id80">[16]</a></td>
</tr>
<tr>
<td>Panama <a class="footnote-reference" href="#id135" id="id81">[33]</a></td>
<td>1998</td>
<td>512</td>
<td>2.5</td>
<td class="r-parent"><span class="r">no</span></td>
<td>2⁶</td>
<td>2⁰</td>
<td><a class="footnote-reference" href="#id119" id="id82">[17]</a></td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Whirlpool <a class="footnote-reference" href="#id134" id="id83">[32]</a></td>
<td>2000</td>
<td>512</td>
<td>50</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>SHA-256 <a class="footnote-reference" href="#id139" id="id84">[37]</a> <a class="footnote-reference" href="#id153" id="id85">[52]</a></td>
<td>2001</td>
<td>256</td>
<td>19</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>RadioGatún <a class="footnote-reference" href="#id140" id="id86">[38]</a></td>
<td>2006</td>
<td>256</td>
<td>?</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Skein <a class="footnote-reference" href="#id141" id="id87">[39]</a></td>
<td>2008</td>
<td>256</td>
<td>8.7</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Blake <a class="footnote-reference" href="#id142" id="id88">[40]</a></td>
<td>2008</td>
<td>256</td>
<td>17</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Grøstl <a class="footnote-reference" href="#id143" id="id89">[41]</a></td>
<td>2008</td>
<td>256</td>
<td>24</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Keccak (SHA-3) <a class="footnote-reference" href="#id144" id="id90">[42]</a></td>
<td>2008</td>
<td>256</td>
<td>16</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>JH <a class="footnote-reference" href="#id145" id="id91">[43]</a></td>
<td>2008</td>
<td>256</td>
<td>20</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>BLAKE2 <a class="footnote-reference" href="#id146" id="id92">[44]</a></td>
<td>2012</td>
<td>256</td>
<td>5.7</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td class="g-parent"><span class="g">yes</span></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<dl class="docutils">
<dt><em>legend:</em></dt>
<dd>
<ul class="first last simple">
<li><em>bit</em>: the number of bits of output</li>
<li><em>cpb</em>: cycles per byte [*]</li>
<li><em>comp</em>: approximate computation required for the attack</li>
<li><em>mem</em>: approximate memory required for the attack</li>
</ul>
</dd>
</dl>
<table class="docutils table table-responsive footnote" frame="void" id="id93" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id4">[*]</a></td>
<td>Cycles per byte were taken from on ebash's <a class="reference external" href="http://bench.cr.yp.to/results-hash.html#amd64-pluton1mn">amd64-pluton1mn</a>, 4096-byte blocks, median measurement, except for Tiger, which was is not measured on that machine and was instead taken from ebash's <a class="reference external" href="http://bench.cr.yp.to/results-hash.html#amd64-h9ivy">amd64-h9ivy</a>, and Panama, which is not measured on ebash. For Panama, I measured it on my laptop (an Intel(R) Core(TM) i5-3427U, which is similar to the ebash <a class="reference external" href="http://bench.cr.yp.to/results-hash.html#amd64-h9ivy">amd64-h9ivy</a> machine) with Crypto++ v5.6.2's implementation of Panama. I also measured MD5, SHA-1, SHA-256, SHA-512, SHA-3-256, SHA-3-512, Tiger, Whirlpool, and RIPEMD-160 on my machine and confirmed that their measurements on my machine were similar to the measurements posted from <a class="reference external" href="http://bench.cr.yp.to/results-hash.html#amd64-h9ivy">amd64-h9ivy</a>.</td>
</tr>
</tbody>
</table>
<p><!-- | Snefru-3 [3]_ | | | | :r:`no` | 2²⁹ | 2⁰ | | :r:`no` | 2⁵⁶ | 2⁰ | | --> <!-- +- - - - - - - - - - - - - - - -+ | +- - - - -+- - - - - - - - - - - -+- - - - - -+- - - - -+ +- - - - - -+- - - - -+- - - - - -+- - - - -+ + --> <!-- | Snefru-4 [3]_ | | | | :r:`no` | ≥2⁴⁵ | 2⁰ | | :y:`maybe` | ≥2⁸⁸ | 2⁰ | | --> <!-- +- - - - - - - - - - - - - - - -+- - - - - -+- - - - - - - - - -+- - - - -+- - - - - - - - - - - -+- - - - - -+- - - - -+- - - - - - -+- - - - - - - - - - - -+- - - - - -+- - - - -+- - - - - - -+ --> <!-- +- - - - - - - - - - - - - - - -+ | +- - - - -+- - - - - - - - - - - -+- - - - - -+- - - - -+- - - - - - -+- - - - - -+- - - - -+- - - - - -+- - - - -+- - - - - - -+ --> <!-- | HAVAL-256-4 | | | | :r:`no` | 2³⁶ | 2⁰ | [12]_ | :g:`yes` | 2²⁵⁴ | 2⁶⁸ | | --> <!-- +- - - - - - - - - - - - - - - -+ | +- - - - -+- - - - - - - - - - - -+- - - - - -+- - - - -+- - - - - - -+- - - - - -+- - - - -+- - - - - -+- - - - -+- - - - - - -+ --> <!-- | HAVAL-256-5 | | | | :y:`maybe` | 2¹²³ | 2⁰ | | :g:`yes` | 2²⁵⁵ | 2⁶⁸ | | --> <span class="target" id="id94"></span></p>
<table class="docutils table table-responsive footnote" frame="void" id="id95" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id16">[†]</a></td>
<td>For MD2, I marked it as "maybe" safe in the collisions column up until 2010 and then marked is as "no". This is even though there are no known collision attacks on them better than brute force. This is because MD2's 128-bit output means the brute force attack takes only 2⁶⁴ comp and negligible memory to find a collision. To do that much comp has become feasible over the last few years. For example, by 2014 the Bitcoin mining network is doing it approximately every 10 minutes <a class="footnote-reference" href="#id147" id="id96">[45]</a>, <a class="footnote-reference" href="#id148" id="id97">[46]</a>!</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id98" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id25">[‡]</a></td>
<td>SHA-0 was considered unsafe beginning in 1995, not because of any published attack on it, nor because the 2⁸⁰ work factor for the brute force collision attack was feasible, but because the NSA had asserted that something was wrong with SHA-0 when they published SHA-1.</td>
</tr>
</tbody>
</table>
<p><span class="target" id="id99"></span></p>
<table class="docutils table table-responsive footnote" frame="void" id="id100" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[§]</td>
<td>RIPEMD-160's 160-bit output means it takes only 2⁸⁰ comp and negligible memory to find a collision. In my estimation this was safe until recently and is now “maybe” safe. See also <a class="footnote-reference" href="#id149" id="id101">[47]</a> and Table 5.1 of <a class="footnote-reference" href="#id150" id="id102">[49]</a>.</td>
</tr>
</tbody>
</table>
<p><!-- XXX Hm, actually maybe 2⁸⁰ is now unsafe! https://twitter.com/josephbonneau/status/436362370785751040 --></p>
</div>
<div class="section" id="discussion">
<h2>Discussion</h2>
<p>The main result of this investigation is that there is a big gap between the historical successes of collision attacks and the almost non-existence successes of pre-image attacks. This is evidence that a cryptosystem invulnerable to collision attacks is much safer than one that is vulnerable to collision attacks (regardless of whether it is vulnerable to pre-image attacks).</p>
<p>Another interesting pattern that I perceive in these results is that <em>maybe</em> sometime between 1996 (Tiger) and 2000 (Whirlpool), humanity learned how to make collision-resistant hash functions, and none of the prominent secure hash functions designed since that era have succumbed to collision attacks. Maybe modern hash functions like SHA-256, SHA-3, and BLAKE2 will never be broken.</p>
<p>Or maybe this is just a 17-year-long hiatus, and in the future we'll discover how to perform collision attacks against the "modern" secure hash functions. Looking in the rearview mirror can't answer that for us.</p>
</div>
<div class="section" id="acknowledgments">
<h2>Acknowledgments</h2>
<p>Thanks to Daira Hopwood, Andreas Hülsing, and Samuel Neves for comments on this note.</p>
<table class="docutils table table-responsive footnote" frame="void" id="id103" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id61">[1]</a></td>
<td><a class="reference external" href="http://cr.yp.to/papers.html#bruteforce">http://cr.yp.to/papers.html#bruteforce</a> Bernstein-2005</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id104" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id62">[2]</a></td>
<td><a class="reference external" href="http://www.springerlink.com/content/qn746388035614r1/">http://www.springerlink.com/content/qn746388035614r1/</a> Knudsen-2007</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id105" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[3]</td>
<td><em>(<a class="fn-backref" href="#id5">1</a>, <a class="fn-backref" href="#id40">2</a>, <a class="fn-backref" href="#id63">3</a>)</em> <a class="reference external" href="http://www.springerlink.com/content/t10683l407363633/">http://www.springerlink.com/content/t10683l407363633/</a> Merkle-1990</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id106" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[4]</td>
<td><em>(<a class="fn-backref" href="#id64">1</a>, <a class="fn-backref" href="#id65">2</a>)</em> <a class="reference external" href="http://www.springerlink.com/content/208q118x13181g32/">http://www.springerlink.com/content/208q118x13181g32/</a> Biham-2008</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id107" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id67">[5]</a></td>
<td><a class="reference external" href="http://eprint.iacr.org/2010/583">http://eprint.iacr.org/2010/583</a> Zhong-2010</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id108" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id66">[6]</a></td>
<td><a class="reference external" href="http://www.springerlink.com/content/v6526284mu858v37/">http://www.springerlink.com/content/v6526284mu858v37/</a> Naito-2006</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id109" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[7]</td>
<td><em>(<a class="fn-backref" href="#id10">1</a>, <a class="fn-backref" href="#id12">2</a>)</em> <a class="reference external" href="http://eprint.iacr.org/2004/199">http://eprint.iacr.org/2004/199</a> Wang-2004 “Collisions for Hash Functions MD4, MD5, HAVAL-128 and RIPEMD”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id110" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id70">[8]</a></td>
<td><a class="reference external" href="http://www.springerlink.com/content/d7pm142n58853467/">http://www.springerlink.com/content/d7pm142n58853467/</a> Sasaki-2009</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id111" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id69">[9]</a></td>
<td><a class="reference external" href="https://eprint.iacr.org/2013/170">https://eprint.iacr.org/2013/170</a> Xie-2013 “Fast Collision Attack on MD5”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id112" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id73">[10]</a></td>
<td><a class="reference external" href="http://www.springerlink.com/content/d382324nl16251pp/">http://www.springerlink.com/content/d382324nl16251pp/</a> Sasaki-2008</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id113" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[11]</td>
<td><em>(<a class="fn-backref" href="#id14">1</a>, <a class="fn-backref" href="#id72">2</a>)</em> <a class="reference external" href="http://academic.research.microsoft.com/Publication/676305/cryptanalysis-of-3pass-haval">http://academic.research.microsoft.com/Publication/676305/cryptanalysis-of-3pass-haval</a> Van-Rompay-2003</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id114" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[12]</td>
<td><a class="reference external" href="http://www.springerlink.com/content/0n9018738x721090/">http://www.springerlink.com/content/0n9018738x721090/</a> Yu-2006</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id115" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id74">[13]</a></td>
<td><a class="reference external" href="http://www.springerlink.com/content/3810jp9730369045/">http://www.springerlink.com/content/3810jp9730369045/</a> Manuel-2008</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id116" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[14]</td>
<td><em>(<a class="fn-backref" href="#id19">1</a>, <a class="fn-backref" href="#id75">2</a>, <a class="fn-backref" href="#id76">3</a>)</em> <a class="reference external" href="http://www.cosic.esat.kuleuven.be/publications/article-2091.pdf">http://www.cosic.esat.kuleuven.be/publications/article-2091.pdf</a> Mendel-2008</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id117" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id21">[15]</a></td>
<td><a class="reference external" href="http://people.csail.mit.edu/yiqun/SHA1AttackProceedingVersion.pdf">http://people.csail.mit.edu/yiqun/SHA1AttackProceedingVersion.pdf</a> Wang-2005b “Finding Collisions in the Full SHA-1”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id118" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id80">[16]</a></td>
<td><a class="reference external" href="http://eprint.iacr.org/2010/016">http://eprint.iacr.org/2010/016</a> Guo-2010</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id119" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id82">[17]</a></td>
<td><a class="reference external" href="http://radiogatun.noekeon.org/panama/PanamaAttack.pdf">http://radiogatun.noekeon.org/panama/PanamaAttack.pdf</a> Daemen-2007 “Producing Collisions for Panama, Instantaneously”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id120" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[18]</a></td>
<td><a class="reference external" href="http://www.win.tue.nl/hashclash/rogue-ca/">http://www.win.tue.nl/hashclash/rogue-ca/</a> Sotirov-2009</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id121" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[19]</td>
<td><em>(<a class="fn-backref" href="#id6">1</a>, <a class="fn-backref" href="#id41">2</a>)</em> <a class="reference external" href="http://link.springer.com/chapter/10.1007%2F3-540-46766-1_11">http://link.springer.com/chapter/10.1007%2F3-540-46766-1_11</a> Biham-1991</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id122" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id8">[20]</a></td>
<td><a class="reference external" href="http://repo.zenk-security.com/Cryptographie%20.%20Algorithmes%20.%20Steganographie/Cryptanalysis%20of%20MD4.pdf">http://repo.zenk-security.com/Cryptographie%20.%20Algorithmes%20.%20Steganographie/Cryptanalysis%20of%20MD4.pdf</a> .. Dobbertin-1995</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id123" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[21]</td>
<td><em>(<a class="fn-backref" href="#id3">1</a>, <a class="fn-backref" href="#id39">2</a>)</em> <a class="reference external" href="https://tools.ietf.org/html/rfc1115">https://tools.ietf.org/html/rfc1115</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id124" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[22]</td>
<td><em>(<a class="fn-backref" href="#id7">1</a>, <a class="fn-backref" href="#id42">2</a>)</em> <a class="reference external" href="https://tools.ietf.org/html/rfc1186">https://tools.ietf.org/html/rfc1186</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id125" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[23]</td>
<td><em>(<a class="fn-backref" href="#id9">1</a>, <a class="fn-backref" href="#id43">2</a>)</em> <a class="reference external" href="http://books.google.com/books?id=9Zi0__jNRvEC&amp;lpg=PA1&amp;ots=NJoLlc8QRz&amp;dq=%E2%80%9CIntegrity%20Primitives%20for%20Secure%20Information%20Systems.%20Final%20Report%20of%20RACE%20Integrity%20Primitives%20Evaluation%20(RIPE-RACE%201040)%2C%E2%80%9D&amp;lr&amp;pg=PA71#v=onepage&amp;q=ripemd&amp;f=false">http://books.google.com/books?id=9Zi0__jNRvEC&amp;lpg=PA1&amp;ots=NJoLlc8QRz&amp;dq=%E2%80%9CIntegrity%20Primitives%20for%20Secure%20Information%20Systems.%20Final%20Report%20of%20RACE%20Integrity%20Primitives%20Evaluation%20(RIPE-RACE%201040)%2C%E2%80%9D&amp;lr&amp;pg=PA71#v=onepage&amp;q=ripemd&amp;f=false</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id126" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[24]</td>
<td><em>(<a class="fn-backref" href="#id11">1</a>, <a class="fn-backref" href="#id44">2</a>)</em> <a class="reference external" href="https://tools.ietf.org/html/rfc1321">https://tools.ietf.org/html/rfc1321</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id127" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[25]</td>
<td><em>(<a class="fn-backref" href="#id13">1</a>, <a class="fn-backref" href="#id45">2</a>, <a class="fn-backref" href="#id71">3</a>)</em> <a class="reference external" href="http://labs.calyptix.com/files/haval-paper.pdf">http://labs.calyptix.com/files/haval-paper.pdf</a> Zheng-1992 “HAVAL – a one-way hashing algorithm with variable length of output”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id128" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[26]</td>
<td><em>(<a class="fn-backref" href="#id15">1</a>, <a class="fn-backref" href="#id46">2</a>)</em> "FIPS PUB 180 / Federal Information Processing Standards Publication 180 / 1993 MAY 11"</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id129" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id17">[27]</a></td>
<td><a class="reference external" href="http://link.springer.com/chapter/10.1007%2F11426639_3">http://link.springer.com/chapter/10.1007%2F11426639_3</a> Biham-2005 “Collisions of SHA-0 and Reduced SHA-1”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id130" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[28]</td>
<td><em>(<a class="fn-backref" href="#id18">1</a>, <a class="fn-backref" href="#id47">2</a>)</em> "GOST 34.11-94, Information Technology Cryptographic Data Security Hashing Function (1994) (in Russian)"</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id131" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[29]</td>
<td><em>(<a class="fn-backref" href="#id20">1</a>, <a class="fn-backref" href="#id48">2</a>)</em> <a class="reference external" href="http://itl.nist.gov/fipspubs/fip180-1.htm">http://itl.nist.gov/fipspubs/fip180-1.htm</a> SHA-1</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id132" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[30]</td>
<td><em>(<a class="fn-backref" href="#id24">1</a>, <a class="fn-backref" href="#id49">2</a>, <a class="fn-backref" href="#id78">3</a>)</em> <a class="reference external" href="http://link.springer.com/chapter/10.1007%2F3-540-60865-6_44">http://link.springer.com/chapter/10.1007%2F3-540-60865-6_44</a> “RIPEMD-160: A Strengthened Version of RIPEMD”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id133" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[31]</td>
<td><em>(<a class="fn-backref" href="#id26">1</a>, <a class="fn-backref" href="#id50">2</a>, <a class="fn-backref" href="#id79">3</a>)</em> <a class="reference external" href="http://link.springer.com/chapter/10.1007/3-540-60865-6_46">http://link.springer.com/chapter/10.1007/3-540-60865-6_46</a> Anderson-1996 “Tiger: A fast new hash function”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id134" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[32]</td>
<td><em>(<a class="fn-backref" href="#id30">1</a>, <a class="fn-backref" href="#id52">2</a>, <a class="fn-backref" href="#id83">3</a>)</em> <a class="reference external" href="http://cryptospecs.googlecode.com/svn/trunk/hash/specs/whirlpool.pdf">http://cryptospecs.googlecode.com/svn/trunk/hash/specs/whirlpool.pdf</a> Barreto-2000 “The WHIRLPOOL Hashing Function”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id135" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[33]</td>
<td><em>(<a class="fn-backref" href="#id27">1</a>, <a class="fn-backref" href="#id51">2</a>, <a class="fn-backref" href="#id81">3</a>)</em> <a class="reference external" href="http://link.springer.com/chapter/10.1007/3-540-69710-1_5">http://link.springer.com/chapter/10.1007/3-540-69710-1_5</a> Daemen-1998 “Fast Hashing and Stream Encryption with Panama”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id136" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id28">[34]</a></td>
<td><a class="reference external" href="http://www.cosic.esat.kuleuven.be/publications/article-81.pdf">http://www.cosic.esat.kuleuven.be/publications/article-81.pdf</a> Rijmen-2002 “Producing Collisions for PANAMA”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id137" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id29">[35]</a></td>
<td><a class="reference external" href="http://radiogatun.noekeon.org/panama/">http://radiogatun.noekeon.org/panama/</a> Daemen-2007 “Producing Collisions for Panama, Instantaneously”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id138" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id68">[36]</a></td>
<td><a class="reference external" href="http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.106.4759">http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.106.4759</a> Wang-2005a “Cryptanalysis of the hash functions MD4 and RIPEMD”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id139" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[37]</td>
<td><em>(<a class="fn-backref" href="#id31">1</a>, <a class="fn-backref" href="#id53">2</a>, <a class="fn-backref" href="#id84">3</a>)</em> <a class="reference external" href="http://csrc.nist.gov/publications/fips/fips180-2/fips180-2.pdf">http://csrc.nist.gov/publications/fips/fips180-2/fips180-2.pdf</a> “FIPS Publication 180-2”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id140" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[38]</td>
<td><em>(<a class="fn-backref" href="#id32">1</a>, <a class="fn-backref" href="#id54">2</a>, <a class="fn-backref" href="#id86">3</a>)</em> <a class="reference external" href="http://radiogatun.noekeon.org/">http://radiogatun.noekeon.org/</a> Bertoni-2006 “The RadioGatún Hash Function Family”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id141" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[39]</td>
<td><em>(<a class="fn-backref" href="#id33">1</a>, <a class="fn-backref" href="#id55">2</a>, <a class="fn-backref" href="#id87">3</a>)</em> <a class="reference external" href="http://www.skein-hash.info/sites/default/files/skein1.3.pdf">http://www.skein-hash.info/sites/default/files/skein1.3.pdf</a> Ferguson-2008 “The Skein Hash Function Family”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id142" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[40]</td>
<td><em>(<a class="fn-backref" href="#id34">1</a>, <a class="fn-backref" href="#id56">2</a>, <a class="fn-backref" href="#id88">3</a>)</em> <a class="reference external" href="https://131002.net/blake/">https://131002.net/blake/</a> Aumasson-2008 “SHA-3 proposal BLAKE”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id143" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[41]</td>
<td><em>(<a class="fn-backref" href="#id35">1</a>, <a class="fn-backref" href="#id57">2</a>, <a class="fn-backref" href="#id89">3</a>)</em> <a class="reference external" href="http://www.groestl.info/">http://www.groestl.info/</a> Gauravaram-2008 “Grøstl – a SHA-3 candidate”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id144" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[42]</td>
<td><em>(<a class="fn-backref" href="#id36">1</a>, <a class="fn-backref" href="#id58">2</a>, <a class="fn-backref" href="#id90">3</a>)</em> <a class="reference external" href="http://keccak.noekeon.org/">http://keccak.noekeon.org/</a> Bertoni-2008 “The Keccak sponge function family”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id145" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[43]</td>
<td><em>(<a class="fn-backref" href="#id37">1</a>, <a class="fn-backref" href="#id59">2</a>, <a class="fn-backref" href="#id91">3</a>)</em> <a class="reference external" href="http://www3.ntu.edu.sg/home/wuhj/research/jh/">http://www3.ntu.edu.sg/home/wuhj/research/jh/</a> Wu-2008 “The Hash Function JH”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id146" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[44]</td>
<td><em>(<a class="fn-backref" href="#id38">1</a>, <a class="fn-backref" href="#id60">2</a>, <a class="fn-backref" href="#id92">3</a>)</em> <a class="reference external" href="https://blake2.net/">https://blake2.net/</a> Aumasson-2012 “BLAKE2: simpler, smaller, fast as MD5”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id147" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id96">[45]</a></td>
<td><a class="reference external" href="https://en.bitcoin.it/wiki/Difficulty">https://en.bitcoin.it/wiki/Difficulty</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id148" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id97">[46]</a></td>
<td><a class="reference external" href="http://bitcoin.sipa.be/">http://bitcoin.sipa.be/</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id149" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id101">[47]</a></td>
<td><a class="reference external" href="http://www.keylength.com/en/3/">http://www.keylength.com/en/3/</a></td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id150" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id102">[49]</a></td>
<td><a class="reference external" href="http://www.ecrypt.eu.org/ecrypt2/documents/D.SPA.20.pdf">http://www.ecrypt.eu.org/ecrypt2/documents/D.SPA.20.pdf</a> Smart-2012 “ECRYPT II Yearly Report on Algorithms and Keysizes (2011-2012)”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id151" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[50]</a></td>
<td><a class="reference external" href="http://www.mail-archive.com/cryptography@metzdowd.com/msg10800.html">http://www.mail-archive.com/cryptography@metzdowd.com/msg10800.html</a> Linus Torvalds email</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id152" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id22">[51]</a></td>
<td><a class="reference external" href="http://oai.cwi.nl/oai/asset/21208/21208B.pdf">http://oai.cwi.nl/oai/asset/21208/21208B.pdf</a> Stevens-2013 “New collision attacks on SHA-1 based on optimal joint local-collision analysis”</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id153" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id85">[52]</a></td>
<td><a class="reference external" href="https://www.google.com/patents/US6829355">https://www.google.com/patents/US6829355</a> SHA-2 patent filed 2001</td>
</tr>
</tbody>
</table>
<table class="docutils table table-responsive footnote" frame="void" id="id154" rules="none">
<colgroup>
<col class="label">
<col>
</colgroup>
<tbody valign="top">
<tr>
<td class="label">[53]</td>
<td><em>(<a class="fn-backref" href="#id23">1</a>, <a class="fn-backref" href="#id77">2</a>)</em> <a class="reference external" href="http://shattered.io/static/shattered.pdf">http://shattered.io/static/shattered.pdf</a> Stevens-2017 “The first collision for full SHA-1”</td>
</tr>
</tbody>
</table>
<p><!-- .. _Leurent-2008: http://www.di.ens.fr/~leurent/files/MD4_FSE08.pdf --> <!-- .. _SHA-3-Zoo: http://ehash.iaik.tugraz.at/wiki/The_SHA-3_Zoo --></p>
<table class="docutils table table-responsive field-list" frame="void" rules="none">
<colgroup>
<col class="field-name">
<col class="field-body">
</colgroup>
<tbody valign="top">
<tr class="field">
<th class="field-name">Author:</th>
<td class="field-body">Zooko Wilcox-O'Hearn</td>
</tr>
<tr class="field">
<th class="field-name">Contact:</th>
<td class="field-body"><a class="reference external" href="mailto:zooko@z.cash">zooko@z.cash</a></td>
</tr>
<tr class="field">
<th class="field-name">Affiliation:</th>
<td class="field-body">Zcash</td>
</tr>
<tr class="field">
<th class="field-name">Revision:</th>
<td class="field-body">2017-02-24</td>
</tr>
<tr class="field">
<th class="field-name">Date:</th>
<td class="field-body">2017-02-24</td>
</tr>
<tr class="field">
<th class="field-name">License:</th>
<td class="field-body"><a class="reference external" href="http://creativecommons.org/licenses/by/4.0/deed.en_US">Creative Commons Attribution 4.0 International License</a></td>
</tr>
</tbody>
</table>
</div>
