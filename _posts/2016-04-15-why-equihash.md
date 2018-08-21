---
ID: 1648
post_title: Why Equihash?
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/why-equihash/
published: true
post_date: 2016-04-15 00:00:00
---
In our <a class="reference external" href="/new-alpha-release-equihash-and-founders-reward/">last blog post</a>, we announced that we have started using Equihash as the proof-of-work for block mining in Zcash (<a class="reference external" href="https://github.com/zcash/zcash/issues/27">#27</a>).

<a class="reference external" href="http://wp.internetsociety.org/ndss/wp-content/uploads/sites/25/2017/09/equihash-asymmetric-proof-of-work-based-generalized-birthday-problem.pdf" target="_blank">Equihash</a> is a Proof-of-Work algorithm devised by Alex Biryukov and Dmitry Khovratovich. It is based on a computer science and cryptography concept called the Generalized Birthday Problem.
<div id="why-are-we-using-it" class="section">
<h2>Why are we using it?</h2>
Equihash has very efficient verification. This could in the future be important for light clients on constrained devices, or for implementing a Zcash client inside Ethereum (like <a class="reference external" href="http://btcrelay.org/">BTC Relay</a>, but for Zcash).

Equihash is a memory-oriented Proof-of-Work, which means how much mining you can do is mostly determined by how much RAM you have. We think it is unlikely that anyone will be able to build cost-effective custom hardware (ASICs) for mining in the foreseeable future.

We also think it is unlikely that there will be any major optimizations of Equihash which would give the miners who know the optimization an advantage. This is because the Generalized Birthday Problem has been widely studied by computer scientists and cryptographers, and Equihash is close to the Generalized Birthday Problem. That is: it looks like a successful optimization of Equihash would be likely also an optimization of the Generalized Birthday Problem.

Nevertheless, we can't know for certain that Equihash is safe against these issues, and we may change the Proof-of-Work again, if we find some flaw in Equihash or if we find another Proof-of-Work algorithm which offers higher assurance.

</div>
<div id="how-can-i-mine" class="section">
<h2>How can I mine?</h2>
The same way as before! Just add <tt class="docutils literal">gen=1</tt> to your config file, or run <tt class="docutils literal">./src/zcashd <span class="pre">-gen</span></tt>.

</div>
<div id="what-are-the-mining-requirements" class="section">
<h2>What are the mining requirements?</h2>
The memory requirements for testnet mining are currently set very low, because the implementation is not optimised. So currently, anyone who was mining before can still mine.

Once we have optimised the implementation (<a class="reference external" href="https://github.com/zcash/zcash/issues/857">#857</a>), we will bump up the memory requirements to around 1 GB of RAM (<a class="reference external" href="https://github.com/zcash/zcash/issues/856">#856</a>), so you will need that much free memory per mining thread.

</div>
<div id="what-s-next" class="section">
<h2>What's next?</h2>
The next step in our use of Equihash is to write an optimised implementation. Once that is done, we will reset the testnet with higher-memory parameters.

Further down the track, our goal is to have the Equihash solver optimised for running on smartphones. We hope that this will greatly aid the decentralization of mining — users could mine Zcash while their phones are plugged in and unused overnight!

Stay tuned for an upcoming blog post about how Equihash works!

</div>