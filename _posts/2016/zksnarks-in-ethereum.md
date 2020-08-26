---
ID: 4983
post_title: zkSNARKs in Ethereum
post_name: zksnarks-in-ethereum
post_date: 2016-07-28 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/zksnarks-in-ethereum/
published: true
tags:
  - Ethereum
  - zkSNARKs
categories:
  - General
---
<p>Over the last week, Zcashers Vitalik Buterin, Andrew Miller, Eran Tromer and myself have been at the <a class="reference external" href="http://initc3.org/events-bootcamp.php">Ethereum/IC3 Bootcamp</a> at Cornell. At the event, we worked with a fantastic team of Cornell students/interns and a member of the Ethereum foundation to bring zkSNARKs to Ethereum for the first time.</p>
<div class="figure">
<img alt="SNARKs in Ethereum Team Photo" src="/wp-content/uploads/2016/07/bootcamp.jpg"/></p>
<p class="caption">(Left to Right) Yuncong Hu, Casey Detrio, Josh Gancher, Sean Bowe, Eran Tromer</p>
</div>
<div class="section" id="snarks">
<h2>SNARKs</h2>
<p>zk-SNARKs are the cryptographic tool underlying Zcash. They are proofs that you have performed a computation over some inputs without revealing all of the inputs. Zcash uses these proofs to verify transactions while protecting users' privacy.</p>
<p>In addition to being great for privacy, they're also great at reducing the verification cost of complicated smart contracts. Since they can be verified quickly, and because the proofs are small, they can protect the integrity of the computation without burdening non-participants.</p>
<p>In our work this week, we extended the Ethereum contract language to efficiently support verification of zkSNARK proofs. Specifically, we added a <cite>snarkverify</cite> precompile (like an opcode) to a fork of <a class="reference external" href="https://github.com/ethcore/parity">Parity</a> which uses libsnark to verify generic proofs.</p>
</div>
<div class="section" id="zerocash-over-ethereum">
<h2>Zerocash over Ethereum</h2>
<p><img alt="Sean Bowe demonstrates the circuit." src="/wp-content/uploads/2016/07/bootcamp_sean.jpg"/></p>
<p>As a demonstration, we used this new zkSNARK verifier in Ethereum to implement a primitive coin mixing contract using a simplified variant of Zerocash -- the academic protocol that Zcash based its implementation on. We call this "baby" ZoE, for Zerocash over Ethereum. The contract allows you to deposit discrete amounts (units of ETH) by inserting a commitment to a "serial number" into a merkle tree maintained by the contract.</p>
<p>In order to withdraw without revealing which commitment you're spending, which would link the withdrawal with the deposit, we use a zkSNARK to prove that <em>we know</em> a commitment inside of the merkle tree of the contract. In order to prevent double-spending, we do so while revealing the serial number, which the contract remembers and prohibits reuse of.</p>
<p>In order to prevent other users from taking the proof and withdrawing without your permission, the proof also authenticates for a withdrawal address (in Ethereum) which is authorized to receive the funds from the contract.</p>
<p>The idea of integrating Zerocash into a currency using a SNARK verification opcode goes back to the original Zerocash paper (Section 6.3 in <a class="reference external" href="https://eprint.iacr.org/2014/349">Zerocash extended version</a>). Following this prescription, it is possible to extend the ZoE contract  to work with the complete Zerocash protocol.</p>
</div>
<div class="section" id="conclusion">
<h2>Conclusion</h2>
<p>We love contributing to both Bitcoin and Ethereum, and look forward to more collaboration with the broader cryptocurrency community. You can look at our group's code <a class="reference external" href="https://github.com/zcash/babyzoe">here</a>.</p>
</div>
