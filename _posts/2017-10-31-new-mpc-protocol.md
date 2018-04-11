---
ID: 1587
post_title: >
  Improved zk-SNARK Multi-party
  Computation Protocol
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/new-mpc-protocol/
published: true
post_date: 2017-10-31 00:00:00
---
<p>zk-SNARKs – the zero-knowledge proofs at the core of Zcash – require a <a class="reference external" href="https://z.cash/technology/paramgen.html">parameter generation ceremony</a> to take place for every statement that you wish to create proofs about. Although privacy is protected by zk-SNARKs unconditionally, if this ceremony is compromised it becomes possible to counterfeit Zcash. It is thus important for us to ensure these parameters are created securely.</p>
<p>Last year, Zcash <a class="reference external" href="/the-design-of-the-ceremony/">performed</a> such a ceremony using a <a class="reference external" href="/snark-parameters/">multi-party computation</a> (MPC) protocol. These protocols have the property that only <em>one</em> party needs to be uncompromised for the resulting parameters to be secure. In other words, in order to compromise the ceremony, <em>every</em> participant needed to be compromised.</p>
<p>However, the protocol we used for the ceremony could not scale beyond a handful of participants. As we continue to upgrade Zcash, we will need to perform more of these setups, so improving the scalability and performance of this protocol is important to us. Also, projects outside Zcash that wish to use zk-SNARKs may need to perform their own setups, so we'd like to make it cheaper and easier for them as well.</p>
<p>Ariel Gabizon, Ian Miers and I have just published a <a class="reference external" href="https://eprint.iacr.org/2017/1050">paper</a> detailing a new MPC protocol which can scale to a practically unbounded number of participants. The paper also includes the strengthened elliptic curve construction, BLS12-381, which we've <a class="reference external" href="/new-snark-curve/">blogged about</a> before.</p>
<div class="section" id="player-exchangeable-mpc">
<h2>Player-exchangeable MPC</h2>
<p>In the <a class="reference external" href="https://eprint.iacr.org/2017/602">original</a> MPC protocol, all participants needed to commit to their share of the "toxic waste" in advance in order to protect against adaptive attacks. This meant that all of the participants needed to be available for the entire duration of the protocol, and nobody could abort without causing the entire protocol to abort. Participants needed to maintain custody of their hardware throughout the process, so this meant the ceremony could not scale beyond a handful of people.</p>
<p>Our new protocol is what we like to call a <em>player-exchangeable MPC</em>. As before, only one participant needs to be honest for the ceremony to be secure. But unlike before, participants join the protocol, do their part and leave immediately. This allows the ceremony to scale to a large number of participants and take place over a longer period of time. It also decreases the surface area of attack for participants and avoids the need for expensive synchronization.</p>
</div>
<div class="section" id="two-phases">
<h2>Two phases</h2>
<p>The original MPC protocol involved three phases of computation. Participants needed to act and then wait for their turn in the next phase. In between the first and second phase, we needed to perform very expensive fast-fourier transforms. As a result of all this, performance of the original MPC was poor.</p>
<p>In the new protocol, we’ve managed to reduce the MPC to two phases. What's more, the first phase is agnostic to the precise zk-SNARK circuit, and so a large communal ceremony can be performed which evaluates this phase for all projects that wish to use zk-SNARKs. The second phase does not involve fast-fourier transforms, which means that MPCs for Zcash and other projects can scale to an unbounded number of participants without overly expensive computations.</p>
<p>We have begun an implementation of this <a class="reference external" href="https://github.com/ebfull/powersoftau">first phase</a> of the multi-party computation ceremony, written in Rust, which uses the new BLS12-381 elliptic curve.</p>
</div>
<div class="section" id="summary">
<h2>Summary</h2>
<p>This new protocol allows for far more secure zk-SNARK parameter generation ceremonies:</p>
<ul class="simple"><li>It allows the ceremony to involve a larger number of participants, with the same property that only one of them needs to be honest to guarantee the parameters are secure.</li>
<li>It allows us to give participants significant flexibility in the hardware and operating system they use to participate. As a result, it allows us to reduce the number of dependencies and code that we must audit.</li>
<li>It greatly reduces the time participants must spend in the ceremony, reducing the surface area of attacks and allowing a broader set of participants to contribute.</li>
<li>It uses a stronger elliptic curve construction which improves security.</li>
</ul><p>We look forward to sharing more details about zk-SNARK parameter generation ceremonies in the near future.</p>
</div>