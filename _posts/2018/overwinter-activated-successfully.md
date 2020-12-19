---
ID: 5017
post_title: Overwinter Activated Successfully
post_name: overwinter-activated-successfully
post_date: 2018-06-26 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/overwinter-activated-successfully/
published: true
tags:
  - governance
  - Overwinter
  - releases
categories:
  - General
---
<p>Overwinter has successfully activated at block 347500!</p>
<p>More information on the Zcash Overwinter protocol upgrade and support is available on the <a href="https://z.cash/upgrade/overwinter.html">Zcash Overwinter Information page</a>. Anyone suspecting issues should monitor the <a href="https://z.cash/support/security/announcements.html">Zcash Security Announcements</a>. </p>
<p>Overwinter also marks the first Zcash implementation of a two-tiered governance model for protocol upgrades. </p>
<p>The first tier is an opt-in upgrade. This means that all nodes on the system have the option to upgrade their node with the latest protocol rules. The intent of the opt-in upgrade is to remove chaos introduced by other governance models where users are forced down a certain path, potentially without their knowledge or consent.</p>
<p>The second tier is advocacy and education. Node operations should be able to make a well-informed decision, within a reasonable amount of time. The Zcash Company advocated for the Overwinter upgrade by educating and working with miners, exchanges, wallets and vendors on their implementations well in advance of the activation. Many of those supporting the upgrade are listed on the <a href="https://z.cash/upgrade/overwinter.html">Overwinter Information page</a>.</p>
<p>In addition to advocacy, we took a number of steps to ensure user safety:</p>
<ul>
<li style="font-weight: 400;">The Zcash Company supported client was updated to, by default, shut down legacy nodes through the “<a href="/blog/release-cycle-update/">end-of-support halt</a>” introduced in release 1.0.9. </li>
<li style="font-weight: 400;">Alerts were sent to all nodes running 1.0.15 or earlier. The alert forced those nodes to enter “safe mode”, lock down wallet RPC methods, and is returning errors so that nodes are aware of the upgrade and can act accordingly. </li>
<li style="font-weight: 400;">The Zcash Company and members of the community have been communicating details of the upgrade through social media, forums and the Z.cash website.</li>
</ul>
<p>Some Zcash nodes may not have received an alert, as in the case where the node is running an old version or 3rd party software such as Zcash4Win. The client still entered safe mode and the user is unable to transact until the software is upgraded. </p>
<p>It should be noted that all funds and private keys are unaffected by the end-of-support halt or by triggering safe mode. It is recommended that nodes simply upgrade to the <a href="https://z.cash/download.html">latest Zcash client software</a> and wait for their nodes to sync at least past the activation block height.</p>
<p>We believe that this governance model should be considered best practice for ensuring safe and well-informed upgrades while maximally preserving user freedom. Thanks to the Zcash Company engineering team’s tireless efforts, the Zcash network succeeded in a solid and safe first upgrade!</p>
