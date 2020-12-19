---
ID: 4863
post_title: Anatomy of A Zcash Transaction
post_name: anatomy-of-zcash
post_date: 2016-11-23 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/anatomy-of-zcash/
published: true
tags:
  - explainers
  - privacy
  - transactions
  - zcash
categories:
  - General
---
<p>Since the successful launch of the Zcash network on <a class="reference external" href="/blog/zcash-begins/">October 28th</a>, we've had an outpouring of interest from miners and users who want to take advantage of the confidentiality and privacy properties enabled in the protocol. When sending or receiving ZEC, the added choice of using shielded or transparent addresses is an important factor for those users. Understanding how these two types are used in a transaction is a suitable place to start to make the most informed choices.</p>
<div class="section" id="the-building-blocks-of-a-transaction">
<h2>The Building Blocks of A Transaction</h2>
<p>The user-facing building blocks of a Zcash transaction can be broken down into sending and receiving addresses, account balances and transaction fees. More complex transaction components are explored in our <a class="reference external" href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">protocol specification</a> so we'll avoid those concepts for now. For sending to shielded addresses, an additional “memo field” component is available but that will be a topic for a future post.</p>
<div class="figure align-center">
<img alt="A high-level skeleton diagram of a Zcash transaction" class="center-image" src="/wp-content/uploads/2016/11/high-level-txn_v3.png"/></p>
<p class="caption">A high-level view of a Zcash transaction</p>
</div>
<p>The diagram above shows the process of sending and receiving ZEC as part of a transaction. The use of shielded addresses - whether sending or receiving - requires the generation of a zero-knowledge proof which allows others to verify a transaction's encrypted data without it being revealed. (More detail on how this works will be discussed in an upcoming post on the inner workings of transactions between shielded addresses.) These addresses always start with a “z” and are sometimes referred to as “z-addrs”. Similarly, the use of transparent addresses require interaction with what is known as a “Transparent Value Pool” (or TVP) and publicly reveals transaction data. These addresses always start with a “t” and are sometimes referred to as “t-addrs”. The transaction fee also passes through the TVP and is therefore always visible on the blockchain. Even though fees are always revealed in a transaction, shielded addresses and value are not affected as shown in the following real Zcash transaction.</p>
<div class="figure align-center">
<img alt="A screenshot from Zchain block explorer showing sending ZEC between shielded addresses" src="/wp-content/uploads/2016/11/shield-shield-txn.png"/></p>
<p class="caption">A screenshot from the Zchain block explorer of a <a class="reference external" href="https://explorer.zcha.in/transactions/35f6674a1691f21aff6a3819467dbba82aaebf061d50c6ac55f39fbeae73b9a6">transaction between shielded addresses</a></p>
</div>
</div>
<div class="section" id="change-addresses">
<h2>Change Addresses</h2>
<p>Like other blockchain protocols, spending from a balance in an address requires sending all of the balance. Therefore, unless you want to send the exact balance to another party, you must split the balance by including a second receiving address you control to accept any balance change. It is possible to simply use the sending address as the change address to prevent the added management of multiple addresses. This, however, is not normally recommended since it would be trivial for someone to build an identity profile based off of transactions sent to and from that single public address. Creating a new address for each transaction has become recommended standard practice in order to obfuscate a user's transactions. Since public transactions link sending and receiving addresses, however, this level of obfuscation is still quite trivial to navigate around and does not provide a meaningful level of privacy.</p>
<p>Thankfully, when sending ZEC from a shielded address, that data is kept private so sending change back to the sending address is permissible. In Zcash, all transactions between shielded addresses look identical so the reuse of shielded addresses is not vulnerable in the same way that transparent addresses are.</p>
</div>
<div class="section" id="sending-between-shielded-and-transparent-addresses">
<h2>Sending Between Shielded and Transparent Addresses</h2>
<div class="figure align-center">
<img alt="A diagram showing differences between sending ZEC to and from shielded and transparent addresses" class="center-image" src="/wp-content/uploads/2016/11/basic-txn-types_v2.png"/></p>
<p class="caption">Properties of sending ZEC between shielded and transparent addresses</p>
</div>
<p>In Zcash, ZEC is the balance unit for how much value an address contains. It differs from purely public blockchain currencies in that a ZEC balance has a different set of properties depending on what address type it is currently held in and the previous address(es) it was sent from. If ZEC is held in a transparent address, its unspent balance is publicly viewable. Regardless of that balance being sent to one or more transparent addresses, shielded addresses or a combination of these types, the output ZEC from a transparent address will be visible. A benefit of sending transparent ZEC to a shielded address is breaking the linkability between future transparent addresses if that's where it ends up again. The action of shielding ZEC is particularly important at these early stages where many wallets (such as mobile wallets) may not yet support shielded addresses due to the resource requirements as explained in a previous blog post on <a class="reference external" href="/blog/software-usability-and-hardware-requirements/">user expectations for hardware and software limitations</a>.</p>
<div class="figure align-center">
<img alt="A screenshot from Zchain block explorer showing sending ZEC from a transparent address to a shielded address" src="/wp-content/uploads/2016/11/transparent-shield-txn.png"/></p>
<p class="caption">A screenshot from the Zchain block explorer of a transaction <a class="reference external" href="https://explorer.zcha.in/transactions/de1d78ee310ba2c9fbeb13881f431fdc8b55aa5f79e61dd3c294177401878f11">shielding ZEC</a></p>
</div>
<p>In the transaction above where a transparent address sends to a shielded address, you can see that this process of shielding ZEC reveals the balance sent and that it is held by shielded addresses. The shielded addresses involved and whether it was sent to one or two shielded addresses remains confidential.</p>
<p>To contrast, a ZEC balance in a shielded address keeps the balance and account address private. If spending to one or more shielded addresses, the value stays private but any transparent addresses on the receiving end will deshield the ZEC and reveal the value received on the blockchain. When deshielding ZEC, the input shielded addresses and whether the value was sent from one or two of these remains confidential.</p>
</div>
<div class="section" id="further-notes-on-more-complex-transactions-and-privacy-implications">
<h2>Further Notes on More Complex Transactions and Privacy Implications</h2>
<p>It should be noted that these examples do not detail the properties of more complex transactions where both transparent and shielded addresses are sending or receiving. With this overview on the basic properties of addresses and spending ZEC balances, however, users can hopefully gain a better perspective on how the transactions work when transacting between any two addresses. Expect future posts on the inner workings of shielded addresses, further considerations on linkability and privacy implications, and details on the more complex transactions. We are eager to promote shielded addresses to improve <a class="reference external" href="https://explorer.zcha.in/statistics/value">stats</a> on their use. While transactions involving shielded addresses require more resources than those with strictly transparent addresses, the improved privacy provided when using them is a clear benefit for financial freedom and is the core improvement Zcash brings as a cryptocurrency.</p>
</div>
