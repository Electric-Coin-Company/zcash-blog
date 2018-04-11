---
ID: 1558
post_title: The Encrypted Memo Field
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/encrypted-memo-field/
published: true
post_date: 2016-12-05 00:00:00
---
<p>As of <a class="reference external" href="/zcash-begins/">October 28, 2016</a>, Zcash is a reality! Anybody with Internet access can <a class="reference external" href="https://z.cash/download.html">download the software</a>, connect to the <a class="reference external" href="https://mainnet.z.cash/">global decentralized network</a>, and send and receive payments, <em>without</em> exposing their confidential transaction metadata to the world.</p>
<p>Note: we have not yet created a user-friendly wallet. The software we're distributing is only for command-line-wielding Linux users. Fortunately many other individuals and companies have already stepped forward to provide <a class="reference external" href="https://zcashblog.wordpress.com/zcash-gui-wallets/">graphical user interfaces</a>.</p>
<p>This blog post is about a little-known but potentially valuable feature of this new protocol.</p>
<div class="section" id="the-encrypted-memo-field">
<h2>The Encrypted Memo Field</h2>
<p>When you receive a Zcash payment from someone else's shielded address to a shielded address of your own, you see the amount of Zcash received, and you see the transaction ID, which allows you to identify this transaction (in its encrypted form) in the blockchain.</p>
<p>You don't learn anything about the sender or about the history of the money you're receiving, and you don't see the sender's address. This is by design — the sender should be able to send you money without necessarily revealing other information about themselves.</p>
<p>However, we realized that senders would sometimes need to communicate information about a specific payment. For example an invoice number or account number that the payment is for, an address to which any refunds should be sent, a note to the recipient, etc.</p>
<p>So we implemented an additional field that is visible to the recipient of a payment, called the “encrypted memo field”. It is always present in every encrypted payment, and is always exactly 512 bytes long. If a sender doesn't specify a memo, then the memo that is sent is all zeroes (before encryption), and if the sender includes a memo shorter than 512 bytes, then the remaining space is padded with zeroes (before encryption).</p>
<p>This padding is necessary for privacy, so that an observer watching the blockchain can't detect differences between different usage patterns of the encrypted memos. It also means that you don't pay a higher transaction fee for including a memo — the cost is already baked in.</p>
<p>The encrypted memo is visible only the to recipient, unless the transaction view key for the transaction gets shared (by the sender or the recipient) with a third party. In that case, the third party who received the transaction view key would be able to see the memo, along with the amount and the recipient address of the transaction in the blockchain. Transaction view keys are already present in the protocol, but are not yet supported in the API.</p>
</div>
<div class="section" id="what-will-people-do-with-this">
<h2>What Will People Do With This</h2>
<div class="figure align-center">
<img alt="a memo field. Remember those?" class="center-image" src="http://blog.z.cash/wp-content/uploads/2016/12/a-memo-field.png"/></div>
<p>We conceived of the encrypted memo field as being basically like the memo space at the bottom of old-fashioned paper checks, but lately we've been wondering: what <em>else</em> will people use this for?</p>
<p>Zcash is the first system which combines the <em>append-only</em> property of blockchains with the <em>selective disclosure</em> property of encryption. Using the memo field you can enter arbitrary data (as long as it fits into 512 bytes) into the global, decentralized Zcash blockchain, and your data will become part of the <em>immutable</em> and <em>append-only</em> ledger, but it will not be <em>visible</em> to anyone else — yet. If you later disclose the transaction view key to someone, then the data will become visible to <em>them</em> in the blockchain. If you were to post the transaction view key publicly, then the data would become visible to the public, still embedded in its original place in the blockchain.</p>
<p>Could this feature be useful for private messaging? Time-stamping? Public records such as land title registries? Securely storing and sharing confidential data such as health records or business records?</p>
<p>I really don't know if the encrypted memo field would be appropriate and effective for those purposes, but as of now, the feature is live and nothing can stop you from experimenting with it. If you do, please let me know what you learn!</p>
</div>
<div class="section" id="return-addresses">
<h2>Return Addresses</h2>
<p>One of the more obvious uses for an encrypted memo field sent within a ZEC payment between shielded addresses is a return or refund address. Merchants may prompt their customers to include a refund address along with a payment in the chance that the product must be returned or a service canceled early. Since the memo isn't required to hold the address from which the payment was sent, this feature could even be used as a cryptographically secured gift receipt. If someone buys their sister a birthday gift from a merchant, the gift giver can include their sister's shielded payment address in the memo field and share the transaction ID with her which holds the encrypted transaction details. She won't know the value of the bracelet but if she finds it doesn't fit right, she can return the product to the merchant with the transaction ID, which the merchant can associate with the product and initiate a refund to the address provided in the memo field.</p>
</div>
<div class="section" id="the-travel-rule">
<h2>The Travel Rule</h2>
<p>Another specific use that we had in mind was satisfying <a class="reference external" href="https://www.sec.gov/about/offices/ocie/aml2007/fincen-advissu7.pdf">The Travel Rule</a>. The Travel Rule is a regulation of <a class="reference external" href="https://en.wikipedia.org/wiki/Financial_Crimes_Enforcement_Network">FinCEN</a> which states that when one financial institution is sending a transaction to another, the sending institution is required to include the identifying information of the customer on whose behalf they are making the payment. It's called the Travel Rule because the identifying information is required to <em>travel with</em> the payment, rather than just being delivered out of band or kept in a database. Financial institutions using Bitcoin (e.g. exchanges like Kraken and Poloniex) face difficulty satisfying this regulation, because you can't really include your customer's personal information in a globally-transparent blockchain!</p>
<p>With Zcash, a financial institution <em>can</em> satisfy that rule, by putting the customer's personal information into the encrypted memo. This makes it visible to the receiving financial institution, but not to unauthorized third parties.</p>
</div>
<div class="section" id="love-notes-in-the-blockchain">
<h2>Love Notes In The Blockchain</h2>
<p>Recently a young woman told me that she had received an encrypted Zcash transaction, and in the memo field, she found a merkletree hash which pointed to a file in the <a class="reference external" href="https://ipfs.io/">IPFS</a> distributed file system. Following that link, she found that the file was a ticket to a special event, overseas, that she and her distant lover had been talking about attending together.</p>
<p>The memo was a love note. A love note which is permanently embedded somewhere in the first few blocks of the Zcash blockchain, but which is visible only to two people. I think that is beautiful.</p>
</div>
<div class="section" id="zmsg">
<h2>zmsg</h2>
<p>Here's a simple program to put memos into the encrypted memo field and to read them out again (if you are the recipient of the enclosing transaction): <a class="reference external" href="https://github.com/whyrusleeping/zmsg">zmsg</a></p>
</div>
<div class="section" id="endless-possibilities">
<h2>Endless possibilities</h2>
<p>While the examples listed in this post highlight some of the exciting ways users, developers and merchants can use the encrypted memo field in Zcash payments, it is only the beginning. We encourage everyone to experiment with this feature and the tools being built around it. You can share your findings and ideas for cool hacks in our <a class="reference external" href="https://forum.z.cash">online community</a>.</p>
</div>