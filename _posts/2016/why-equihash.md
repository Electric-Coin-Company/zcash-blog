---
ID: 4969
post_title: Why Equihash?
post_name: why-equihash
post_date: 2016-04-15 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/why-equihash/
published: true
tags:
  - Equihash
  - mining
categories:
  - General
---
<p>In our <a class="reference external" href="/blog/new-alpha-release-equihash-and-founders-reward/">last blog post</a>, we announced that we have started using Equihash as the proof-of-work for block mining in Zcash (<a class="reference external" href="https://github.com/zcash/zcash/issues/27">#27</a>).</p>
<p><a class="reference external" href="https://web.archive.org/web/20180304090546/http://wp.internetsociety.org/ndss/wp-content/uploads/sites/25/2017/09/equihash-asymmetric-proof-of-work-based-generalized-birthday-problem.pdf" target="_blank" rel="noopener noreferrer">Equihash</a> is a Proof-of-Work algorithm devised by Alex Biryukov and Dmitry Khovratovich. It is based on a computer science and cryptography concept called the Generalized Birthday Problem.</p>
<div id="why-are-we-using-it" class="section">
<h2>Why are we using it?</h2>
<p>Equihash has very efficient verification. This could in the future be important for light clients on constrained devices, or for implementing a Zcash client inside Ethereum (like <a class="reference external" href="http://btcrelay.org/">BTC Relay</a>, but for Zcash).</p>
<p>Equihash is a memory-oriented Proof-of-Work, which means how much mining you can do is mostly determined by how much RAM you have. We think it is unlikely that anyone will be able to build cost-effective custom hardware (ASICs) for mining in the foreseeable future. <strong>*</strong></p>
<p>We also think it is unlikely that there will be any major optimizations of Equihash which would give the miners who know the optimization an advantage. This is because the Generalized Birthday Problem has been widely studied by computer scientists and cryptographers, and Equihash is close to the Generalized Birthday Problem. That is: it looks like a successful optimization of Equihash would be likely also an optimization of the Generalized Birthday Problem.</p>
<p>Nevertheless, we can't know for certain that Equihash is safe against these issues, and we may change the Proof-of-Work again, if we find some flaw in Equihash or if we find another Proof-of-Work algorithm which offers higher assurance.</p>
</div>
<div id="how-can-i-mine" class="section">
<h2>How can I mine?</h2>
<p>The same way as before! Just add <tt class="docutils literal">gen=1</tt> to your config file, or run <tt class="docutils literal">./src/zcashd <span class="pre">-gen</span></tt>.</p>
</div>
<div id="what-are-the-mining-requirements" class="section">
<h2>What are the mining requirements?</h2>
<p>The memory requirements for testnet mining are currently set very low, because the implementation is not optimised. So currently, anyone who was mining before can still mine.</p>
<p>Once we have optimised the implementation (<a class="reference external" href="https://github.com/zcash/zcash/issues/857">#857</a>), we will bump up the memory requirements to around 1 GB of RAM (<a class="reference external" href="https://github.com/zcash/zcash/issues/856">#856</a>), so you will need that much free memory per mining thread.</p>
</div>
<div id="what-s-next" class="section">
<h2>What's next?</h2>
<p>The next step in our use of Equihash is to write an optimised implementation. Once that is done, we will reset the testnet with higher-memory parameters.</p>
<p>Further down the track, our goal is to have the Equihash solver optimised for running on smartphones. We hope that this will greatly aid the decentralization of mining — users could mine Zcash while their phones are plugged in and unused overnight!</p>
<p>Stay tuned for an upcoming blog post about how Equihash works!</p>
<p><em><strong>*&nbsp;</strong><span class="blob-code-inner blob-code-marker-addition">As of May 2018, <span class="x x-first x-last">Zcash's Equihash parameters have </span>been implemented in ASIC miners.<span class="x x-first"> We're still evaluating whether we think Equihash will resist ASIC implementation long-term. </span></span>Read the <a href="/blog/zcash-company-statement-on-asics/">Zcash Company Statement on ASICs</a> for more information.</em></p>
</div>
