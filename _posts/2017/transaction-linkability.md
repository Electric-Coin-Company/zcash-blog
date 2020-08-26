---
ID: 4965
post_title: Transaction Linkability
post_name: transaction-linkability
post_date: 2017-01-25 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/transaction-linkability/
published: true
tags:
  - explainers
  - privacy
  - transactions
categories:
  - General
---
<p>Having the two types of addresses within Zcash (transparent and shielded) is an advantage which allows users to have more flexibility with how they store and transact ZEC. The dynamic between transparent and shielded addresses, however, presents a level of increased complexity for transactions containing both types (i.e. shielding ZEC by sending from a transparent to a shielded address or deshielding ZEC by sending from a shielded to a transparent address).</p>
<p>If all Zcash transactions used shielded addresses (which we hope will someday become the norm), then the complexities introduced with the two types of addresses disappear and privacy would strengthen for everyone in the ecosystem. Until then, understanding privacy implications such as transaction linking will be helpful for users interested in maintaining maximum control over the visibility of their transaction details.</p>
<p>This post will outline some privacy considerations while using Zcash with its current support for both transparent and shielded addresses and some solutions users can employ in such situations.</p>
<div class="section" id="where-does-zcash-introduce-linkability">
<h2>Where does Zcash introduce linkability?</h2>
<div class="section" id="transparent-addresses">
<h3>Transparent Addresses</h3>
<p>Knowing that transparent addresses publicly disclose transaction details on the Zcash blockchain, we can assume a degree of linkability between a string of transactions using this type of address, similar to the linkability seen in bitcoin transactions.</p>
<p>But what happens when shielded addresses are sprinkled into the mix? Thankfully, shielded addresses in Zcash indeed break linkability when used properly.</p>
<div class="figure align-center">
<img alt="Comparing transaction series: three transparent addresses vs a shielded address sandwiched between two transparent addresses" class="center-image high-res-image" src="/wp-content/uploads/2017/01/t-vs-z-links.png"/></p>
<p class="caption">Shielded addresses can de-link transparent addresses <a class="footnote-reference" href="#id4" id="id1">[1]</a></p>
</div>
<p>The mere use of shielded addresses by merchants accepting ZEC payments and by your friends provides an increased level of privacy for you, too! In the above example, the transaction series where Bob uses a shielded address (b) breaks the link between Alice and Carol. To help understand these properties, we created the following transactions which mimic the examples above: <a class="reference external" href="https://explorer.zcha.in/transactions/548a0ee2d59821624a13abe841c6a86eec85fec101eabe152254aa565a3abe9f">Alice sends 15 ZEC (minus fee) to transparent Bob</a> and <a class="reference external" href="https://explorer.zcha.in/transactions/ca69d489c5f1df34f4143d898284ade9f7a8df1f50955d6c77628c82b1702085">transparent Bob sends 10 ZEC to Carol</a> compared with <a class="reference external" href="https://explorer.zcha.in/transactions/7bf9d70ba43624c7fc88319b1caf9281b400ad5b3607024fb14e234fedb85854">Alice sends 15 ZEC (minus fee) to shielded Bob</a> and <a class="reference external" href="https://explorer.zcha.in/transactions/87570f1d30841ea41ea4cbf5a85f1eb6a6879b5fbc0c1d9c6e360702e0af0e45">shielded Bob sends 10 ZEC to Carol</a>.</p>
<p>So even if you or your friends must use transparent addresses for one reason or another, others using shielded addresses (whether they mean to or not) break down the direct linkability that would otherwise exist with exclusively transparent addresses.</p>
</div>
<div class="section" id="linking-values">
<h3>Linking Values</h3>
<p>The above method where Bob de-links Alice and Carol simply by using a shielded address isn’t 100% reliable for every situation, however.</p>
<p>To explain why, let’s first highlight a property of transactions which include both address types: when transparent addresses shield ZEC (t → z) or when shielded addresses deshield ZEC (z → t), the values sent to or received from transparent addresses are public even though those values are masked in the shielded address part of the transaction. We can observe this property in the transaction series above where Bob uses a shielded address but the transparent addresses used by Alice and Carol still reveal the value sent and received.</p>
<div class="figure align-center">
<img alt="A diagram showing the possibile value linkability in a transaction series even when a shielded address is used in between transparent addresses" class="center-image high-res-image" src="/wp-content/uploads/2017/01/z-linkability.png"/></p>
<p class="caption">A shielded address might not protect against value linkability in some cases</p>
</div>
<p>Now, let’s consider the condition where Bob sends the full balance received from Alice to Carol and therefore has no change output. If Alice’s public output X and Carol’s public input Y are equal (or X equals Y minus two standard transaction fees) and that value is unique enough to other public values stored in the Zcash blockchain, there is a degree of association between Alice and Carol. You can see this example in the following transactions: <a class="reference external" href="https://explorer.zcha.in/transactions/20d2742d56ab03012ea92d1521db22b8224ff5fe52218686e1cee3fda609bcde">Alice sends 15 ZEC (minus .0001 ZEC fee) to shielded Bob</a> and <a class="reference external" href="https://explorer.zcha.in/transactions/12255ca035f59e2373ba16b820763de788536a73812b2b025df11e46757e96f3">shielded Bob sends 14.9999 ZEC (minus .0001 ZEC fee) to Carol</a>.</p>
<p>Further, this association increases the closer in blocktime Alice’s public output and Carol’s public input are recorded.  For example, in the above transactions, Alice sends ZEC to Bob in block number 50374 and Bob sends ZEC to Carol in block number 50378. This makes it easier to link the values than if Bob instead transacted with Carol in block number 111583.</p>
<p>To mitigate this, Bob should be aware when deshielding a value equal to one recently received from a transparent address. Zcash wallets might even consider implementing a feature to allow automatic detection of potential of linking past and future transactions when deshielding ZEC. <a class="footnote-reference" href="#id5" id="id2">[2]</a></p>
</div>
<div class="section" id="unique-transaction-fees">
<h3>Unique Transaction Fees</h3>
<p>Another linking possibility regards the use of transaction fees. Most wallets use a standard fee to pay miners (.0001 ZEC). In a previous post covering basic <a class="reference external" href="/blog/anatomy-of-zcash/">Zcash transaction anatomy</a>, we showed how fee outputs are always transparent even with shielded addresses. While this doesn’t reveal much to the public if a standard fee value is used, addresses which consistently pay unique fees could be linked.</p>
<p>The solution here is to simply use standard transaction fees!</p>
</div>
</div>
<div class="section" id="reducing-linkability-by-reducing-complexity">
<h2>Reducing Linkability By Reducing Complexity</h2>
<p>While the advantages of supplying both transparent and shielded addresses to users allows for more options <a class="footnote-reference" href="#id6" id="id3">[3]</a>, there is no doubt that sending ZEC between them introduces complexities which affect individual’s financial privacy. The most concrete solution to avoiding transaction linkability is simply using and requesting others use shielded addresses, which in turn strengthens the community’s overall privacy. The Zcash core development team has priorities to support growth in shielded address use and call on third party services to consider ways which make shielded addresses easier to use as well. We’re just at the beginning of this exciting new ecosystem and are looking forward to seeing privacy for all strengthen over time.</p>
<table class="docutils footnote" frame="void" id="id4" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>In transaction series <em>b</em>, we use a question mark to indicate the value received by Bob's shielded address even though it seems exactly 14.9999 ZEC would have been received. This is because it's possible that an additional shielded input and/or output was included in the transfer but we would not be able to see this on the blockchain.</td>
</tr>
</tbody>
</table>
<table class="docutils footnote" frame="void" id="id5" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id2">[2]</a></td>
<td>This value linkability is much more likely in situations where users are sending between their own addresses rather than between different users. In the example used, Alice and Bob might actually be the same person sending between their own transparent and shielded addresses.</td>
</tr>
</tbody>
</table>
<table class="docutils footnote" frame="void" id="id6" rules="none">
<colgroup>
<col class="label"/>
<col/></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id3">[3]</a></td>
<td>While <a class="reference external" href="/blog/zcash-private-transactions/">shielded addresses</a> offer the privacy features which distinguish Zcash from purely public blockchain networks, the transparent addresses provide (at least for now) a relief in <a class="reference external" href="/blog/software-usability-and-hardware-requirements/">resource requirements</a> along with familiar functionality to previously launched cryptocurrencies.</td>
</tr>
</tbody>
</table>
</div>
