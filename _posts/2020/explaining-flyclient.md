---
ID: 9421
post_title: Explaining FlyClient
post_name: explaining-flyclient
post_date: 2020-03-27 17:05:18
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/explaining-flyclient/
published: true
tags:
  - heartwood
  - network upgrade
categories:
  - General
  - Technical
---
<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>One of the key improvements in the <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/introducing-heartwood/">Heartwood upgrade</a> is FlyClient support, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zips.z.cash/zip-0221" target="_blank">ZIP 221</a>. In this post, we’ll explain the importance of FlyClient, how this research came about and what we are excited about in the months ahead.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>Importance of FlyClient</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>FlyClient (ZIP 221) provides a more efficient method for light-client block-header verification and, therefore, has the potential to increase the utility and addressable market for Zcash.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>“Blockchain ledgers get pretty big pretty fast,” explains Lucianna Kiffer, one of the coauthors of the FlyClient paper. “FlyClient proofs are a way to prove that you know the whole ledger is valid using as little information as you can.”</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For Proof-of-Work protocols like Zcash, downloading and verifying the entire blockchain takes time and computational energy. This means that clients with limited resources, such as mobile phones or older computers, cannot verify the blockchain history without relying on a full node. FlyClient solves an important part of this issue with a novel approach to block header verification. It “requires downloading only a logarithmic number of block headers while storing only a single block header between executions” (Bünz, Kiffer et al).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>FlyClient enables light client use-cases and a class of cross-chain interoperability efforts like <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://defirate.com/tzec-token/" target="_blank">tZEC</a>, an Ethereum-compatible ZEC token. A class of decentralized cross-chain protocols rely on light-client verification. For example, tZEC will implement light-client verification of the Zcash blockchain inside an Ethereum smart contract. This is also a potentially useful building block in improving shielded mobile wallets because it allows them to rely less on centralized backend servers.<em>&nbsp;</em></p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>FlyClient research</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>To understand FlyClient, you need to understand NIPoPoWs, and to understand NIPoPoWs you have to go back to the original <a href="https://bitcoin.org/bitcoin.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Bitcoin whitepaper</a>.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>FlyClient research stems from Simplified Payment Verification, or SPV. SPV is a concept introduced in the original Satoshi paper. “It is possible to verify payments without running a full network node. A user only needs to keep a copy of the block headers of the longest proof-of-work chain, which he can get by querying network nodes until he's convinced he has the longest chain, and obtain the Merkle branch linking the transaction to the block it's timestamped in.”</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>SPV is more efficient than downloading an entire blockchain, but it has its limitations. SPV for Bitcoin is relatively straightforward; a mobile client needs only to check the proofs of work. “But for blockchains that come with faster blocks than Bitcoin, or if you want to have a mobile client that supports lots of coins, that's still not enough,” explains Zcash Foundation Board Chair Andrew Miller. To tackle some of the shortfalls of SPV, Miller, along with Aggelos Kiayias and Dionysis Zindros, introduced a new primitive called Non-Interactive Proofs of Proof-of-Work — NIPoPoW for short.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>NIPoPoWs are succinct proofs that require only a single message between the prover and the verifier of the transaction. NiPoPoW is a generic term for a category of protocols that compress blockchain transaction histories for light clients. NIPoPoWs were an improvement on previous SPV approaches. Non-interactive proofs are more efficient than interactive proofs because a non-interactive proof can be checked offline without requiring back-and-forth interrogations (interactions) with a full node.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>NIPoPoWs can differ in their implementations of the proofs. The original NIPoPoW implementation relied on finding and verifying “superblocks.” In PoW blockchains, some blocks are much more difficult than others to solve; these are called superblocks. While superblock NIPoPoWs were an improvement on SPV, they work under a very specific set of constraints, such as constant difficulty and no adversaries or dishonest attackers. Again Miller states, “A lot of the work has been to relax these assumptions. FlyClient is an example of this.”</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>FlyClient is an improvement on NIPoPoWs because it works with variable difficulty or hashrate. “Personally, I think FlyClient is an awesome idea. There’s a lot of history of cryptography that’s behind FlyClient. It’s inspired by prior work done with NIPoPoWs and zero-knowledge research,” says Dionysis Zindros, coauthor of the NIPoPoW paper.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a aria-label=" (opens in a new tab)" href="https://eprint.iacr.org/2019/226.pdf" target="_blank" rel="noreferrer noopener">FlyClient</a> research began as part of an internship project at Visa Research. It was started by Benedict Bünz and Loi Lui in the summer of 2017, and Kiffer joined the team the following summer. FlyClient was <a aria-label=" (opens in a new tab)" href="https://www.youtube.com/watch?v=vuzYwutBqjY" target="_blank" rel="noreferrer noopener">presented at Zcon1</a> in July 2019 and will be published in the 2020 <a aria-label=" (opens in a new tab)" href="https://www.computer.org/csdl/proceedings-article/sp/2020/349700b040/1i0rIpXE5gY" target="_blank" rel="noreferrer noopener">IEEE Symposium on Security and Privacy</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>“It can certainly be improved upon, but it works pretty well. ... Fundamentally, we are hopeful that there are instances where a future version of FlyClient could also work on Proof-of-Stake or DAG-based protocols,” Kiffer explains.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>How FlyClient fits into Zcash</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>FlyClient is one technology among other possibilities that can improve network capacity, light-client support and scalability. ECC’s <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/ecc-scaling-research-2019-research-development-milestones/">Scalability research</a> includes both long-range speculative research such as our work on <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/halo-recursive-proof-composition-without-a-trusted-setup/">Halo</a> and a new horizontally scalable architecture, as well as making continued pragmatic incremental improvements, such as the shorter block target time of Blossom and FlyClient support in Heartwood.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Heartwood will enable better cross-chain interoperability and better mobile wallet functionality, thanks in large part to FlyClient. “One of the biggest benefits of the [FlyClient] protocol is that it is super simple, in terms of what it takes to implement it. This is important for open systems that need to be audited by a lot of people. There are lots of use cases; from using your phone to check if a transaction went through to verifying balances cross-chain,” Kiffer says.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>From ECC CEO Zooko Wilcox: “I'm excited about the potential of FlyClient for cross-chain interop with smart contract blockchains.”</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> Special thanks to Lucianna Kiffer, Andrew Miller and Dionysis Zindros for reviewing this post. ZIP 221 was authored by Ying Tong Lai, James Prestwich, Georgios Konstantopoulos, and Jack Grigg. Parity Technologies contributed significantly to the implementation.  </p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:spacer {"height":28} -->
<div style="height:28px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>For the past four years, ECC has established a reputation of shipping quality, production-ready code. We are proud of our regular and reliable release schedule, having already begun work on NU4. Heartwood is a mandatory network upgrade designed to improve interoperability and privacy. If you are a miner or network node, please stay tuned for more information regarding the Heartwood activation date. If you have any questions, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://discord.gg/PgcDjbm" target="_blank">reach out to us</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":4} -->
<h4>Useful links</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><a href="https://bitcoin.org/bitcoin.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Bitcoin: Peer-to-peer Electronic Cash, Satoshi Nakamoto</a><br><a href="https://eprint.iacr.org/2017/963.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Non-Interactive Proofs of Proof of Work (Paper)</a>, <a href="https://nipopows.com/">website</a><br><a href="https://eprint.iacr.org/2019/226.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">FlyClient: Super-Light Clients for Cryptocurrencies</a><br><a href="https://decryptionary.com/dictionary/simplified-payment-verification/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Simplified Payment Verification, Decryptionary</a><br></p>
<!-- /wp:paragraph -->