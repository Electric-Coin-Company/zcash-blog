---
ID: 5946
post_title: >
  Zcash Reference Wallet Light Client
  Protocol
post_name: >
  zcash-reference-wallet-light-client-protocol
post_date: 2019-01-07 12:00:57
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/zcash-reference-wallet-light-client-protocol/
published: true
tags:
  - Wallet
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>This is the third installment in our series about the progress and development of the Zcash reference wallet; we invite you to look back at previous articles about <a href="https://z.cash/blog/introducing-the-zcash-reference-wallet/">our goals and what we’re building</a> as well as <a href="https://z.cash/blog/zcash-reference-wallet-design/">user experience, interface and styling.</a>  This article builds on those topics, with a discussion about the protocol.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p><em>Note: the reference wallet, along with the work described in this post, is ongoing and subject to updates. ﻿</em></p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>A reference implementation is concrete and functioning code, proving that a concept can work. Recall that <a href="https://z.cash/upgrade/sapling/">Sapling</a> made shielded transactions computationally feasible for low-capacity devices, such as smartphones. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Zcash shielded transactions can work on mobile devices. Our reference wallet and light client library proves that. Light clients are important, because users with low-capacity devices can maintain security assurance about the Zcash network and verify transactions.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Interacting components﻿</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The Zcash reference wallet is a light client. Light clients help users access and interact with a blockchain in a secure and decentralized way without having to sync the full blockchain.&nbsp;Light clients are serviced by a full node server that handles those services. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For security reasons, the light client holds the spending key and generating transactions. This ensures that the owner is in charge of the funds in the wallet, and the server cannot spend the funds without permission. The server is responsible for keeping up with the blockchain data, verifying that transactions happened safely, and servicing many light clients by providing them relevant information. <br /></p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Higher standards for privacy ﻿</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>The typical server can see the details of shielded transactions. This information includes the sender, receiver, and amount. They use that to forward transactions relevant to their clients. For Zcash, this can be done by giving a server the viewing keys to the light clients' addresses they service. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>We want to prevent servers from learning what and how a light client spends or receives funds, to protect the privacy of our users. So, we are working on an alternative solution.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>The first version of the reference wallet will not meet these goals, since the server will know which transactions are being spent by a given light client. But until they are spent the server will not know which transactions are received by a particular light client.</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>Preserving inbound privacy</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>Our design pre-processes blocks on the blockchain so that a light client can then scan through all the information itself. This is tricky since the reference wallet only uses shielded addresses. Since every shielded transaction is encrypted, light clients need to try decrypting every one on the network. If they do not, they might not see that a transaction has sent successfully or miss detecting new incoming transactions. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>This is bandwidth-intensive. To optimize the performance, we: </p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>pass along only sapling shielded transactions</li><li>scan blocks only after sapling activation </li><li>download the transaction memo field on demand </li></ul>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>The memo field is ~70% of a Zcash block. Shielded transactions pad the memo field to reduce distinctive features that could be used to identify them, even if the memo field is not used. Zcash blocks can be trial decrypted the rest of the block to find out the sender, receiver, and amount without decrypting the memo field. To achieve a 70% improvement in bandwidth, we decided to have light clients only decrypt the non-memo parts of a shielded address at first. This makes memo fields second-class citizens, and light clients will reveal which transactions are of interest if they request a specific transaction's memo. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>This is our solution for now. We plan to validate this approach and exploring other approaches in order to improve the user experience and in particular to make sure that using the memo field is useful and secure.</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>For further information, check out the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/gtank/zips/blob/light_payment_detection/zip-XXX-light-payment-detection.rst" target="_blank">protocol specification,</a> <a href="https://github.com/str4d/librustzcash/tree/note-detection">client side code,</a> and <a href="https://github.com/zcash-hackworks/lightwalletd" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">server side code</a>. </p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>Warning: it's a work in progress so the code is unstable. We do not recommend builds off of it. <br /></p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h2>What's next?</h2>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>We will continue to share our progress in these upcoming posts:</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul><li>Development: build methodology and target devices. </li><li>Future work: what's next for the reference wallet. </li></ul>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>Subscribe to the <a href="https://z.cash/blog/">Zcash blog</a> for further updates and other company news. <br /></p>
<!-- /wp:paragraph -->