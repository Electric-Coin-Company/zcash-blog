---
ID: 3312
post_title: Completion of the Sapling MPC
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/completion-of-the-sapling-mpc/
published: true
post_date: 2018-08-14 21:01:21
---
Zcash's next major upgrade, codenamed Sapling, will be <a href="https://blog.z.cash/whats-new-in-sapling/">activated later this year</a>. One of our final goals before activation is the completion of a <a href="https://en.wikipedia.org/wiki/Secure_multi-party_computation">multi-party computation</a> ceremony which produces the <a href="https://z.cash/technology/paramgen.html">public parameters</a> that our shielded transactions depend on.

We're happy to announce the completion of this ceremony! In total, nearly 200 people contributed either directly to the ceremony or to its development, coordination and review. We're including the final parameters in our 2.0.0 release of Zcash later this week.
<p style="text-align: center;"><img class="alignnone wp-image-3331" src="https://blog.z.cash/wp-content/uploads/2018/08/neal-300x300.jpg" alt="" width="175" height="175" /> <img class="alignnone wp-image-3332" src="https://blog.z.cash/wp-content/uploads/2018/08/hudson-300x225.jpg" alt="" width="233" height="175" /> <img class="alignnone wp-image-3333" src="https://blog.z.cash/wp-content/uploads/2018/08/andrew-300x169.jpg" alt="" width="311" height="175" /></p>
<p style="text-align: center;"><em><sup>Images from three Powers of Tau participants: (from left) <a href="https://twitter.com/NealJayu/status/934804507271319554" target="_blank" rel="noopener">Neal Jayu</a>, <a href="https://twitter.com/hudsonjameson/status/930994082444447746" target="_blank" rel="noopener">Hudson Jameson</a> and <a href="https://motherboard.vice.com/en_us/article/gy8yn7/power-tau-zcash-radioactive-toxic-waste" target="_blank" rel="noopener">Andrew Miller and Ryan Pierce</a></sup></em></p>

<h2>Ceremonies</h2>
Zcash's underlying zero-knowledge proofs require some system parameters to be constructed. If these parameters are compromised, an adversary could create counterfeit Zcash coins. In our original launch of Zcash, we defended against this by <a href="https://z.cash/blog/the-design-of-the-ceremony.html">deploying</a> a multi-party computation protocol. The protocol has the property that only one of its participants must be honest in order for the final parameters to be secure.

In the original ceremony, we only had six participants due to scalability issues of the protocol. In addition, due to the sensitivity of the process to protocol aborts, participants did not apply a wide diversity of individual countermeasures to defend against compromise.

Last year, we published a <a href="https://eprint.iacr.org/2017/1050">new protocol</a> for constructing the parameters which is designed to scale to a large number of participants. Unlike the original protocol, a participant can contribute to the ceremony at any time, and they do not need to be in custody of secrets during the entire duration of the ceremony.

Additionally, the new protocol is split into two pieces: a circuit-agnostic phase called the <strong>Powers of Tau</strong>, and a circuit-specific phase that we <a href="https://blog.z.cash/sapling-mpc/">announced</a> several months ago. This allows the broader public to take advantage of the parameters we produced in order to build their own zk-SNARK protocols with scalable MPCs.
<h2>Powers of Tau</h2>
The Zcash Foundation <a href="https://z.cash.foundation/blog/powers-of-tau/">facilitated</a> and hosted the Powers of Tau ceremony, which took place between November 2017 and April 2018. It accepted 87 contributions from cryptographers and members of the community. Only one of these contributions needs to be honestly constructed for the parameters in this phase to be secure.

The diversity of this ceremony was significant. Participants used a wide variety of hardware and operating systems, and many destroyed their hardware afterward. Anyone was allowed to participate either by asking directly or publicly requesting to participate via a mailing list.

Most of the participants <a href="https://github.com/ZcashFoundation/powersoftau-attestations">wrote</a> about their experience and the unique countermeasures they deployed. Andrew Miller and Ryan Pierce famously <a href="https://motherboard.vice.com/en_us/article/gy8yn7/power-tau-zcash-radioactive-toxic-waste">flew in a plane with radioactive material</a> to seed their random number generator. Filippo Valsorda wrote an <a href="https://github.com/FiloSottile/powersoftau">independent implementation</a> of the ceremony code in Go. Devrandom developed a <a href="https://github.com/devrandom/trust-rust">trusted build environment</a> for the Rust code.

You can read more about this ceremony <a href="https://z.cash.foundation/blog/conclusion-of-powers-of-tau/">here</a>, along with instructions for how to verify its results.
<h2>Sapling MPC</h2>
The Zcash Company hosted the MPC for constructing Sapling's final zk-SNARK parameters. We <a href="https://blog.z.cash/sapling-mpc/">announced</a> the ceremony in May and accepted contributions through early August. In all, this ceremony accepted <a href="https://github.com/zcash-hackworks/sapling-mpc/wiki">over 90 contributions,</a> of which only one must be honestly constructed for the success of this phase.

The final parameters are now available <a href="https://storage.googleapis.com/sapling-mpc/params">here</a>. You can verify the parameters using the <code>verify</code> utility in the <a href="https://github.com/zcash-hackworks/sapling-mpc/blob/master/src/bin/verify.rs">sapling-mpc repository</a>. Just as in the Powers of Tau ceremony, we applied a random beacon which you can read about in the <a href="https://lists.z.cash.foundation/pipermail/zapps-wg/2018/000380.html">zapps-wg mailing list</a>.

All of the participants can run this verifier and check that it outputs a hash that their software produced when they contributed to the ceremony. This allows them to confirm that the final parameters include their contribution. These hashes are also listed, along with the participants, <a href="https://github.com/zcash-hackworks/sapling-mpc/wiki">here</a>.
<h2>Conclusion</h2>
We're now ready to move ahead with the Sapling upgrade. The parameters produced by these ceremonies are historic: The Powers of Tau and the Sapling MPC are the largest multi-party computations ever performed.

We'd like to thank the community for participating and improving the quality and security of Zcash and all protocols that build on top of zk-SNARKs.

We'd also like to thank Jason Davies and Ian Munoz for their efforts in coordinating the ceremonies, and the Zcash Foundation for hosting the Powers of Tau.