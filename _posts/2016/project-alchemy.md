---
ID: 4932
post_title: Introducing Project Alchemy
post_name: project-alchemy
post_date: 2016-09-19 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/project-alchemy/
published: true
tags:
  - Ethereum
categories:
  - General
---
<div class="figure align-center">
<p class="caption">Bridging Zcash and Ethereum</p>
</div>
<p>The technical innovation that Zcash is contributing to cryptocurrency is the introduction of reliably private transactions on the blockchain through the application of zero-knowledge proofs. However, much of the value in this ecosystem comes from projects building on each other's strengths. The open, programmable platform that Ethereum introduced is inspiring developers to build new systems that were not possible before. Our team has also been inspired to start brainstorming potential applications.</p>
<p>One of the projects we're looking forward to working on is codenamed <cite>Project Alchemy</cite>. This will be a Zcash-Ethereum integration that will enable a decentralized exchange between the two blockchains. The core component we're focused on first is a cross-chain <cite>Order</cite> that will allow decentralized order execution.</p>
<p>Here’s the basic outline of how it would work: Sellers will be able to publish an Ethereum contract called an <cite>Order</cite>, and anyone can fulfill it by sending out an appropriately formatted Zcash transaction. The funds the initiator wants to exchange will be essentially held in escrow by the smart contract while they wait for a buyer to match them. A buyer will be able to create a Zcash transaction that may contain the destination address, and the validity of this transaction will be verified by the Ethereum contract before the funds are released to complete the trade.</p>
<p>An implementation of a bridge for Bitcoin-to-Ether exchange already exists in <a class="reference external" href="https://github.com/ethereum/btcrelay">BTC Relay</a>, so we are planning to model an exchange for Zcash along these lines <a id="id1" class="footnote-reference" href="#id2">[1]</a>. There are several steps necessary to further develop this idea. One component is an implementation of the BLAKE2b hash function in Solidity, which is necessary to check Zcash’s proof of work — this <a class="reference external" href="https://github.com/tjade273/eth-blake2">has already been written</a>. The hash function will be used to implement an Equihash verifier. Once we can verify Zcash’s proof of work, we can create an example contract template for the <cite>Order</cite> logic. From there, we would need UI components to place, discover, and fulfill orders on the two blockchains.</p>
<p>The small but dedicated Zcash team is currently devoting our time and energy toward launching a secure, usable open blockchain. We don’t have the capacity to build out all of the things we'd like to see exist right away, but we’re excited to start developing projects like this after launch.</p>
<p>Please join us in discussing projects like this on our <a class="reference external" href="https://forum.z.cash/">Forum</a> or <a class="reference external" href="https://inviteme.z.cash/">Slack</a> channels (including <tt class="docutils literal">#alchemy</tt> for this project).</p>
<table id="id2" class="docutils footnote" frame="void" rules="none">
<colgroup>
<col class="label"> </colgroup>
<colgroup>
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>The same building blocks with minor modifications will also allow Bitcoin-Ethereum decentralized exchange, thus enabling currency to flow between the three systems through a decentralized market-price mechanism.</td>
</tr>
</tbody>
</table>
