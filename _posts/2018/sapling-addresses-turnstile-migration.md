---
ID: 5036
post_title: 'Sapling Addresses &amp; Turnstile Migration'
post_name: sapling-addresses-turnstile-migration
post_date: 2018-09-11 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/sapling-addresses-turnstile-migration/
published: true
tags:
  - explainers
  - monetary supply
  - privacy
  - Sapling
  - sprout
  - transactions
categories:
  - General
  - Technical
---
The <a href="https://z.cash/upgrade/sapling.html">Sapling network upgrade</a> is a major feature enhancement to the Zcash network targeted to activate on October 28th, 2018. We've <a href="/blog/whats-new-in-sapling/">outlined</a> the usability and security improvements coming with Sapling but now it's time to take a closer look at what they mean for users and ecosystem services. This is the first of a short series on Sapling features in order to clarify expectations and boost understanding.
<h2>Sapling Addresses</h2>
The current version of Zcash supports the original Sprout shielded address which start with "zc". These addresses infamously require around 1.5 gigabytes of computer memory and 40 seconds to create a zero-knowledge transaction, a severe limitation in their usability.

Upon activation, there will be a new type of shielded address to support the <a href="/blog/cultivating-sapling-faster-zksnarks/">improved efficiency of Zcash's cryptography</a> introduced in Sapling. These Sapling shielded addresses start with a "zs" and are slightly shorter in length (78 characters vs Sprout's 95 characters). While we don't anticipate the shorter address to enhance usability significantly, the time and memory requirements to create transactions will. To do the same function, Sapling shielded addresses take only a few seconds and 40 megabytes of memory on a modern computer. This equates to a time reduction of over 90% and a memory reduction of over 97%!
<h2>Migrating From Sprout</h2>
Sprout shielded addresses will be supported for the foreseeable future; however, users should migrate funds to Sapling addresses to keep up with ecosystem support. Expect third-party services to take advantage of Sapling improvements in the weeks and months after activation.
<h3>Monetary Auditing</h3>
In addition to moving funds to the more efficient Sapling addresses, the migration will act as a monetary auditing mechanism. The trade-off between shielding value and auditing the circulating supply raise valid concerns. Like any valuable asset, preserving the scarcity of ZEC is an important driver of long-term, sustainable value. For example, if gold counterfeiters could successfully sell fools' gold, the perceived loss in scarcity would drive the value down over time.

Zcash engineers have gone through great lengths to protect the network from any deviation in the expected ZEC in circulation. We recommend reading about Zcash's <a href="https://z.cash/technology/paramgen.html">public parameters</a> to understand counterfeiting risks and mitigation techniques. Regardless of how low the probability might be, taking the extra step to detect counterfeit coins is a valuable reassurance.
<h3>Sapling Turnstile</h3>
To audit existing shielded ZEC, we've implemented a process we call the <em>Sapling turnstile</em>. Users will be required to send funds held in old Sprout shielded addresses to transparent addresses before sending to new Sapling shielded addresses. There will be no way to send ZEC directly between Sprout and Sapling shielded addresses using the <code>zcashd</code> RPC. To understand how Zcash transactions work between transparent and shielded addresses, read <a href="/blog/anatomy-of-zcash/">Anatomy of a Zcash Transaction</a>.

<img class="aligncenter size-medium wp-image-3449" src="/wp-content/uploads/2019/06/turnstile-300x179.png" alt="Diagram showing the Sapling turnstile" width="300" height="179">

Deshielding ZEC by sending funds from a shielded address to transparent address will link the value to the transparent address. This brings up some important privacy considerations for users. Most importantly, only deshield to unused transparent addresses and never use them again. We explain more about these considerations in our <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html">Sapling turnstile documentation</a>.

It is also worth noting that this migration method allows sending ZEC back into Sprout shielded addresses from transparent addresses. As of this post, there is no roadmap for deprecating Sprout shielded addresses but discussions around this topic are ongoing.

We recommend all Sprout shielded addresses be replaced with Sapling shielded addresses after activation. Use the privacy recommendations linked above for migrating funds. Not only do Sapling shielded addresses provide a richer feature set but migrating also contributes to auditing the Zcash monetary supply.

Look out for future blog posts which will cover new features enabled in Sapling shielded addresses like HD wallets, diversified addresses, full viewing keys and more.