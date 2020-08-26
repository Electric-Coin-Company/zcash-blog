---
ID: 4931
post_title: Pay-to-sudoku Revisited
post_name: pay-to-sudoku-revisited
post_date: 2017-06-08 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/pay-to-sudoku-revisited/
published: true
tags:
  - cryptography
  - ZKCP
  - zkSNARKs
categories:
  - General
---
<p>Last year, I created a project called <a class="reference external" href="https://github.com/zcash/pay-to-sudoku">pay-to-sudoku</a> which was the world's first implementation of a <a class="reference external" href="https://en.bitcoin.it/wiki/Zero_Knowledge_Contingent_Payment">zero-knowledge contingent payment</a> (ZKCP). ZKCPs were invented in 2011 by Gregory Maxwell, and are a clever cryptographic trick that allows people to trade information and value atomically over a blockchain. Gregory was also kind enough to help me <a class="reference external" href="/blog/science-roundup/">demonstrate it</a> to Financial Cryptography 2016!</p>
<p>In pay-to-sudoku, one person (the "buyer") can pay another person (the "seller") to solve a Sudoku puzzle. The seller solves the puzzle and encrypts the solution with a key that is then hashed. Using a zero-knowledge proof ― in this case, a zk-SNARK using libsnark ― the seller constructs a proof that they have an encrypted solution to the puzzle, and that knowledge of a particular SHA256 hash will permit decryption.</p>
<p>The buyer proceeds to submit a payment to the blockchain that allows the seller to redeem some funds in exchange for revealing the SHA256 preimage (the key). When the seller does this, the buyer can decrypt.</p>
<p>In order to achieve this with a zk-SNARK, the buyer is responsible for constructing a common reference string (CRS) that allows the seller to evaluate a proof. Campanelli, Gennaro, Goldfeder and Nizzardo have just published a <a class="reference external" href="http://stevengoldfeder.com/papers/ZKCSP.pdf">new paper</a> that identifies a flaw in the way pay-to-sudoku uses the PGHR construction implemented in libsnark. In particular, it assumes that the CRS has correct algebraic structure. It also does not check that certain elements of the CRS  that need to be non-zero for zero-knowledge to hold are indeed non-zero. This gives the buyer an opportunity to violate zero-knowledge and obtain information about the solution without paying for it. They also note that <em>even if these checks were carried out</em> it is still not completely clear that zero-knowledge holds.</p>
<p>Interestingly, Zcash's public parameters are not vulnerable to this kind of malicious setup because the <a class="reference external" href="https://github.com/zcash/mpc#transcript-verification">multi-party computation transcript</a> guarantees the correctness of the CRS structure, and enables proving that zero-knowledge holds <em>even if all of the participants of the MPC were dishonest</em>. See our <a class="reference external" href="http://eprint.iacr.org/2017/602.pdf">whitepaper</a> for details. This is pointed out by the paper as well.</p>
<p>There are several mitigating steps that can be taken when using a third-party CRS. The most secure way would be, just as we did with Zcash's public parameters, to generate the CRS  using our multi-party computation protocol. This guarantees zero-knowledge even if this protocol is carried out by <em>just one player</em>; .e.g. the buyer in the case of ZKCP. Alternatively, simply not allowing incorrect structure in the CRS is sufficient to defend against the particular attacks described in the paper. As an additional precaution, verify the proof after you construct it!</p>
<p>The paper additionally proposes some other interesting ideas, such as an extension of the concept of a ZKCP to the purchase of digital services rather than digital goods (like sudoku solutions).</p>
