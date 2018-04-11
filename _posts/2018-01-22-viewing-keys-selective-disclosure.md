---
ID: 2355
post_title: 'Selective Disclosure &#038; Shielded Viewing Keys'
author: Paige Peterson
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/viewing-keys-selective-disclosure/
published: true
post_date: 2018-01-22 15:42:39
---
Encryption is an important tool to control access to personal and business data. In many cases where private data must be shared with select people such as a long distance family member or business associate, employing simple document encryption allows securely sharing private data in less private forms of communication like email. Commonly, one party will encrypt the documents with a password that is also used to decrypt the document by the second party. This password is either already known by everyone who requires access or is shared via a different channel like a phone call or more secure messaging platform.
<div id="viewing-keys-selective-disclosure-granularity" class="section">
<h2>Viewing Keys &amp; Selective Disclosure Granularity</h2>
The encrypted contents of shielded transactions in Zcash have a similar property that individuals can selectively disclose the data from a specific transfer. More broadly, a viewing key may also be provided to disclose all transactions for a given shielded address.

The context of the data disclosure can determine which method someone may prefer to use. For example, the owner of a yoga studio may prefer to disclose their payment address's viewing key to their accountant for keeping track of all revenue while disclosing individual transactions involving merchandise sales to the employee in charge of inventory. Like sharing passwords to decrypt sensitive documents, the channel in which a user shares viewing keys and transaction disclosures is important to consider to make sure only the intended parties gain access. Additionally, anyone you share viewing keys or transaction disclosures with can share further or even make them public so it's important that you trust who you give access to.

</div>
<div id="watch-addresses" class="section">
<h2>Watch addresses</h2>
</div>
&nbsp;
<div id="watch-addresses" class="section">

<img class="aligncenter size-full wp-image-2358" src="https://blog.z.cash/wp-content/uploads/2018/01/key-separation.png" alt="" width="719" height="279" />

Some Zcash users prefer to store their private spending keys offline for increased security. That way even if their accounts get hacked or their online devices get stolen, their Zcash is still safe. However, it also prevents them from being able to see incoming transactions going to the address associated with that spending key. With viewing keys, they can keep the viewing key online so that they can see the transaction activity, while keeping the spending key safely offline.

</div>
<div id="current-implementation-and-future-plans" class="section">
<h2>Current implementation and future plans</h2>
<img class="aligncenter wp-image-2359 size-full" src="https://blog.z.cash/wp-content/uploads/2018/01/vk-pd-public.png" alt="What the public sees" width="505" height="455" />

<img class="aligncenter wp-image-2360 size-full" src="https://blog.z.cash/wp-content/uploads/2018/01/vk-pd-vkowner.png" alt="What data the owner of a viewing key for a specific address sees" width="505" height="454" />

<img class="aligncenter size-full wp-image-2361" src="https://blog.z.cash/wp-content/uploads/2018/01/vk-pd-pdowner.png" alt="What data the owner of a payment disclosure for a specific transaction sees" width="505" height="454" />

At version 1.0.14, Zcash supports viewing key capability for tracking incoming transactions. Tracking outgoing transactions introduces a slightly trickier problem which is proposed to be addressed in the Sapling network upgrade.

Additionally at version 1.0.14, Zcash supports the creation of payment disclosures for transactions sent from a wallet. This can be beneficial when proving that a payment to an address was sent. The current implementation is an experimental feature which means a user must explicitly turn it on. You can check out the <a class="reference external" href="https://github.com/zcash/zcash/blob/master/doc/payment-disclosure.md">payment disclosure documentation</a> for more information about usability and security considerations of this feature and for instructions on how to use it.

We look forward to offering more complete implementations of viewing keys and selective dislosure in the coming releases and upgrades. We're excited to hear about how third-parties are using these features so please let us know how you're working with them. Developers or users with questions can reach out in the <a class="reference external" href="https://chat.zcashcommunity.com">community chat</a>.

</div>