---
ID: 3256
post_title: 'What&#8217;s New in Sapling'
author: Sean Bowe
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/whats-new-in-sapling/
published: true
post_date: 2018-07-13 22:03:46
---
The next major upgrade of Zcash, codenamed Sapling, is scheduled to activate in October 2018. The specific block height has not yet been determined.

Sapling represents over two years of protocol design and engineering with cryptographic breakthroughs that improve the performance and functionality of shielded (encrypted) transactions. Currently, most Zcash transaction use transparent addresses that function in the same way as Bitcoin. This is largely due to the computational cost of encrypting transactions. With Sapling, we move one (giant) step closer to moving toward the ubiquity of shielded addresses.
<h2>Performance for Shielded Transactions</h2>
<h4>Changes</h4>
Today, if you create a new z-address it'll look something like this:
<pre><span class="pl-s">zcA6qngiR3U7HxYopyTWkaDLwYBd83D5MT7Jb9gpgTzPLMZytzRbtdPP1Syv4RvRgHeoZrJWSask3DyfwXG9DGPMWMvX7aC</span></pre>
This is called a <em>Sprout </em>z-address because it was introduced in our original "Sprout" release of Zcash. These addresses start with "zc".

A z-address generated after Sapling activation will look something like this:
<pre><span class="blob-code-inner"><span class="pl-s">zs1z7rejlpsa98s2rrrfkwmaxu53e4ue0ulcrw0h4x5g8jl04tak0d3mm47vdtahatqrlkngh9sly</span></span></pre>
This new, shorter address starts with "zs" and is called a <em>Sapling</em> z-address. The legacy Sprout z-addresses will continue to function after Sapling activates, but will later be deprecated in favor of this new address.
<h4>Implications</h4>
Payments involving the new Sapling z-addresses can be constructed in as little as a few seconds and with only 40 megabytes of memory. Exchanges, mobile wallet wallet providers, vendors and other 3rd parties will now be able to support shielded addresses.

The increased use of shielded addresses will improve the effective privacy for the entire network.
<h2>Decoupled Spend Authority</h2>
<h4>Changes</h4>
All shielded transactions require the creation of a <a href="https://z.cash/technology/zksnarks.html">zero-knowledge proof</a>. Today, the hardware that constructs the proof must also be in possession of the spending key that authorizes the transaction. Sapling changes this by allowing the hardware that constructs the proof to be independent from the hardware that signs for the transaction.
<h4>Implications</h4>
Enterprises can perform an inexpensive signature step in a trusted environment while allowing a another computer, not trusted with the spending key, to construct the proof. Additionally, hardware wallets can support shielded addresses by allowing the connected computer to construct the proof without exposing the spending key to that machine.
<h2>Improved keys</h2>
<h4>Changes</h4>
Shielded addresses currently support an <a href="https://blog.z.cash/viewing-keys-selective-disclosure/">incoming viewing key</a>. The holder of an incoming viewing key for a shielded address are able to see the value of all incoming transactions and the memo field. They cannot see the sending address and cannot spend the funds.

Sapling extends the capability of the viewing key to include visibility into outgoing transactions for a shielded address. Visibility includes the transaction value, memo field and target address.
<h4>Implications</h4>
Viewing keys allow owners of shielded addresses the ability to view transaction details without exposing their private spending key. Additionally, these can be shared with trusted third parties for compliance, auditing or for other reasons. Currently, only incoming transactions are viewable.
<h2>Efficient wallets with many z-addresses</h2>
<h4>Changes</h4>
Sapling z-addresses come with a feature which allows trillions of addresses to receive payments simultaneously with no additional performance cost on the receiving end. All of these addresses are unlinkable with each other.
<h4>Implications</h4>
Currently, exchanges and merchants must pay a computational penalty to receive on large numbers of z-addresses. The new Sapling z-addresses allow these businesses to create large numbers of distinct and unlinkable z-addresses for their clients.
<h1>Follow our progress</h1>
We're excited about the potential for the Sapling upgrade and for making shielded payments faster and easier for our users! We'll keep you updated about the activation date <a href="https://z.cash/upgrade/sapling.html">here</a> along with resources and tips for users dealing with the upgrade.