---
ID: 4972
post_title: >
  An Update on Integrating Zcash on
  Ethereum (ZoE)
post_name: zcash-eth
post_date: 2017-01-19 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/zcash-eth/
published: true
tags:
  - Ethereum
  - smart contracts
  - zkSNARKs
categories:
  - General
---
<p><em>Members of the Ethereum R&amp;D team and the Zcash Company are collaborating on a research project addressing the combination of programmability and privacy in blockchains. This joint post is being concurrently posted on the</em> <a class="reference external" href="https://blog.ethereum.org/2017/01/19/update-integrating-zcash-ethereum/">Ethereum blog</a>, <em>and is coauthored by Ariel Gabizon (Zcash) and Christian Reitwiessner (Ethereum).</em></p>
<p>Ethereum’s flexible smart contract interface enables a large variety of applications, many of which have probably not yet been conceived. The possibilities grow considerably when adding the capacity for privacy.</p>
<p>Imagine, for example, an election or auction conducted on the blockchain via a smart contract, such that the result can be verified by any observer of the blockchain, but the individual votes or bids are not revealed. Another setting is that of selective disclosure; for example, providing users the ability to prove they are in a certain city without disclosing their exact location.</p>
<p>The key to adding such capabilities to Ethereum is zero-knowledge succinct non-interactive arguments of knowledge (zk-SNARKs) - precisely the cryptographic engine underlying Zcash.</p>
<p>One of the goals of the Zcash company, codenamed <a class="reference external" href="/blog/project-alchemy/">Project Alchemy</a>, is to enable a direct decentralized exchange between Ethereum and Zcash. Connecting these two blockchains and teams, one focusing on programmability, and the other on privacy, seems the natural way to bring to life applications requiring both.</p>
<p>As part of the Zcash/Ethereum-collaborative effort, Ariel Gabizon from Zcash visited Christian Reitwiessner from the Ethereum hub at Berlin a few weeks ago. The highlight of the visit is a proof of concept implementation of a zk-SNARK verifier written in Solidity, based on pre-compiled Ethereum contracts implemented for the Ethereum C++ client. This complements <a class="reference external" href="/blog/zksnarks-in-ethereum/">Baby ZoE</a> where a zk-SNARK precompiled contract was written for Parity - the Ethereum Rust client. The difference is that we only added tiny cryptographic primitives (elliptic curve multiplication, addition and pairing) and did the rest in Solidity. This allows for a much greater flexibility and enables using a variety of zk-SNARK constructions without requiring a hard fork (see more details later on). We tested this code by successfully verifying a real privacy-preserving Zcash transaction, on a testnet of the Ethereum blockchain. The verification took only 42 milliseconds, which shows that such precompiled contracts can be added and the gas costs for using them can be made to be quite affordable.</p>
<div id="what-can-be-done-with-such-a-system" class="section">
<h2>What can be done with such a system</h2>
<p>The Zcash system can be reused on Ethereum to create shielded custom tokens. Such tokens already allow many applications like voting (more on that later) or a simple auction where buyers do not learn the others’ bids.</p>
<p>If you want to try compiling the proof of concept, you can use the following commands. If you need help, hop on to <a class="reference external" href="https://gitter.im/ethereum/privacy-tech">https://gitter.im/ethereum/privacy-tech</a></p>
<pre class="code literal-block">git clone https://github.com/scipr-lab/libsnark.git

cd libsnark
sudo PREFIX=/usr/local make NO_PROCPS=1 NO_GTEST=1 NO_DOCS=1 CURVE=ALT_BN128 
   FEATUREFLAGS="-DBINARY_OUTPUT=1 -DMONTGOMERY_OUTPUT=1 -DNO_PT_COMPRESSION=1" 
   lib install
cd ..
git clone --recursive -b snark https://github.com/ethereum/cpp-ethereum.git
cd cpp-ethereum
./scripts/install_deps.sh &amp;&amp; cmake . -DEVMJIT=0 -DETHASHCL=0 &amp;&amp; make eth
cd ..
git clone --recursive -b snarks https://github.com/ethereum/solidity.git
cd solidity
./scripts/install_deps.sh &amp;&amp; cmake . &amp;&amp; make soltest
cd ..
./cpp-ethereum/eth/eth --test -d /tmp/test
# And on a second terminal:
./solidity/test/soltest -t "*/snark" -- --ipcpath   /tmp/test/geth.ipc  --show-messages
</pre>
<p>We also discussed various aspects of integrating zk-SNARKs into the Ethereum blockchain, on which we now expand.</p>
<h2>Deciding what precompiled contracts to define</h2>
<p>Recall that a SNARK is a short proof of some property, and what is needed for adding the privacy features to the Ethereum blockchain is that clients have the ability to verify such a proof.</p>
<p>In all recent constructions, the verification procedure consists solely of operations on elliptic curves. Specifically, the verifier requires scalar multiplication and addition on an elliptic curve group; but also, a heavier operation called a bilinear pairing.</p>
<p>As mentioned <a class="reference external" href="https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/">here</a>, implementing these operations directly in EVM is too costly. Thus, we want to implement pre-compiled contracts that perform these operations. Now, the question we debated was - what level of generality these pre-compiled contracts should aim for.</p>
<p>The security level of the SNARK corresponds to the parameters of the curve. Roughly, the larger the curve order is, and the larger something called the embedding degree is, the more secure the SNARK based on this curve. On the other hand, naturally, the larger these quantities are, the more costly the operations on the corresponding curve. Thus, a contract designer using SNARKs may wish to choose these parameters according to their own desired efficiency/security tradeoff. This is one argument for implementing a pre-compiled contract with a high level of generality, where the contract designer can choose from a large family of curves. We indeed began by shooting for a high level of generality - where the description of the curve is given as part of the input to the contract. In such a case, a smart contract would be able, for example, to perform addition in any elliptic curve group.</p>
<p>A complication with this approach is assigning gas cost to the operation - you must assess, merely from the description of the curve, and with no access to a specific implementation, how expensive a group operation on that curve would be (in the worst case). A somewhat less general approach is to allow all curves from a given family. We noticed that when working with the Barreto-Naehrig (BN) family of curves, one can assess roughly how expensive the pairing operation will be given the curve parameters, as all such curves support a specific kind of optimal Ate pairing. Here's a <a class="reference external" href="https://drive.google.com/file/d/0BwDmGb8qpc8RMEhBMlR5VHE3bEU/view?usp=sharing">sketch</a> of how such a precompile would work and how the gas cost would be computed.</p>
<p>We learned a lot from this debate, but ultimately, decided to "keep it simple" for this proof of concept; and to implement contracts for operations on the specific curve currently used by Zcash. We did this by using wrappers of the corresponding functions in the <a class="reference external" href="https://github.com/scipr-lab/libsnark">libsnark</a> library, also used by Zcash. We note that we could have simply used a wrapper for the entire SNARK verification function currently used by Zcash - as was done in the above mentioned Baby ZoE project. However, the advantage of explicitly defining elliptic curve operations is enabling using a wide variety of SNARK constructions, which, again, all have a verifier working by some combination of the three mentioned elliptic curve operations.</p>
<h2>Reusing the Zcash setup for new anonymous tokens and other applications</h2>
<p>As you might have heard, using SNARKs requires a <a class="reference external" href="/blog/the-design-of-the-ceremony/">complex setup phase</a> in which the so-called public parameters of the system are constructed. The fact that these public parameters need to be generated in a secure way every time we want to use a SNARK for a particular circuit significantly hinders the usability of SNARKs. (Simplifying this setup phase is an important goal that we gave some thought to but didn’t have any success in so far).</p>
<p>On the other hand, the good news is that someone desiring to issue a token supporting privacy-preserving transactions can simply reuse the public parameters that have already been securely generated by Zcash. The reason for this is that the Zcash circuit which is used to verify privacy-preserving transactions is not inherently tied to one currency or blockchain. Rather, one of its explicit inputs is the root of a Merkle tree that contains all the valid notes of the currency; and so, this input can be changed according to the currency one wishes to work with. Moreover, if it is rather easy to start a new anonymous token, you can already accomplish many tasks that do not look like tokens at a first glance. For example, suppose we wish to conduct an anonymous election to choose a preferred option amongst two. We can issue an anonymous custom token for the vote, and send one coin to each voting party. Since there is no “mining”, it will not be possible to generate tokens in any other way. Now each such party sends their coin to one of two addresses according to their vote. The address with a larger final balance corresponds to the election result.</p>
<h2>Other applications</h2>
<p>A non-token-based system that is rather simple to build allows for “selective disclosure”: You can, for example, constantly post an encrypted message containing your physical location to the blockchain (perhaps with other people’s signatures to prevent spoofing). If you use a different key for each message, you can reveal your location only at a certain time by revealing the key. With zk-SNARKs, though, you can prove that you were in a certain area without revealing where exactly you have been: Inside the zk-SNARK, you decrypt your location and show that it is inside the area. Because of the zero-knowledge property, everyone can verify that fact but nobody can retrieve your actual location.</p>
<h2>The work ahead</h2>
<p>Truly achieving the mentioned functionalities - creating anonymous tokens and verifying Zcash transactions on the Ethereum blockchain, will require implementing other elements used by Zcash in Solidity. For the first, we must have an implementation of tasks performed by nodes on the Zcash network such as updating the note commitment tree. For the second, we need an implementation of the equihash proof of work algorithm used by Zcash in Solidity. Otherwise, transactions can be verified as valid in themselves, but we do not know whether the used notes existed on the Zcash blockchain or whether the transaction was actually sent to the Zcash blockchain. Fortunately, such an implementation was <a class="reference external" href="https://github.com/ConsenSys/Project-Alchemy">written</a>; however, its efficiency needs to be improved in order to be used in practical applications.</p>
<p><em>Acknowledgement</em>: We thank Sean Bowe for technical assistance. We also thank Sean and Vitalik Buterin for helpful comments, and Ming Chan for editing.</p>
</div>
