---
ID: 9280
post_title: 'New Releases: 2.1.1 and hotfix 2.1.1-1'
post_name: new-releases-2-1-1-and-hotfix-2-1-1-1
post_date: 2020-02-07 04:55:05
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-releases-2-1-1-and-hotfix-2-1-1-1/
published: true
tags:
  - hotfix
  - releases
categories:
  - General
---
<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>New soft fork</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>On December 31, 2019, Michael Davidson disclosed to us a vulnerability that could be used to cause consensus failure in the network: Nodes would permanently reject blocks based on their timestamps using subjective information. This information could be influenced by an attacker that (partially) isolates the node on the network, potentially tricking a miner or mining pool into rejecting a valid chain. An attacker could have strategically exploited this issue to 51% attack some nodes’ view of the chain and perform double-spending attacks.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We’ve addressed this in a new hotfix release (zcashd v2.1.1-1), which changes how nodes enforce timestamp requirements on block headers. We urge miners and pools to upgrade as soon as possible. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The identifier CVE-2020-8806 has been assigned to this issue.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Timing sidechannel fixed</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The PING and REJECT issues disclosed to us in September 2019 (by Dan Boneh, Kenneth Paterson and Florian Tramèr) and fixed in the earlier 2.0.7-3 release relied on a difference in the network data returned by a victim node. But in fact, an equivalent timing issue existed where the time offset between messages could have been used to tie together a suspected victim's address with an IP address. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The issue was simultaneously discovered by the team disclosing the PING and REJECT issues and the ECC engineering team, and so credit for discovery is shared.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The way Zcashd handled transactions was upgraded in <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-0-7-3/">2.0.7-3</a> (released September 25, 2019) so as to close this issue for new transactions received over the network.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We've addressed how blocks are processed in this release (zcashd v2.1.1) to close this issue for new blocks received over the network.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The identifier CVE-2020-8807 has been assigned to this issue.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Fix for incorrect banning of nodes during syncing</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>After activation of the Blossom network upgrade, a node that is syncing the block chain from before Blossom would incorrectly ban peers that send it a Blossom transaction. This resulted in slower and less reliable syncing (<a href="https://github.com/zcash/zcash/issues/4283" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#4283</a>). zcashd v2.1.1-1 also fixes this problem.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>z_mergetoaddress stabilization</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The RPC command "z_mergetoaddress" is now stabilized and can be used without enabling experimental features. This RPC allows users to merge funds from their various payment addresses into a single address. See <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://zcash.readthedocs.io/en/latest/rtd_pages/payment_api.html#z-mergetoaddress" target="_blank">this ReadTheDocs entry</a> for more information about how to use this command.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Option parsing behavior</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Command line options are now parsed strictly in the order in which they are specified. It used to be the case that "-X -noX" ends up, unintuitively, with X set, as "-X" had precedence over "-noX". This is no longer the case. Like for other software, the last specified value for an option will hold.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Low-level RPC changes</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bare multisig outputs to our keys are no longer automatically treated as incoming payments. As this feature was only available for multisig outputs for which you had all private keys in your wallet, there was generally no use for them compared to single-key schemes. Furthermore, no address format for such outputs is defined, and wallet software can't easily send to it. These outputs will no longer show up in "listtransactions", "listunspent", or contribute to your balance, unless they are explicitly watched (using "importaddress" or "importmulti" with hex script argument). "signrawtransaction*" also still works for them.<br></p>
<!-- /wp:paragraph -->