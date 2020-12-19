---
ID: 9533
post_title: 'New Release: 2.1.2'
post_name: new-release-2-1-2
post_date: 2020-04-23 17:30:43
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-2-1-2/
published: true
tags:
  - releases
categories:
  - General
---
<!-- wp:heading {"level":3} -->
<h3>Heartwood testnet activation</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release supports the activation of <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/introducing-heartwood/">Heartwood</a> on testnet, with an activation height of 903800, slated to occur on May 6, 2020. Please upgrade to this release, or any subsequent release, in order to follow the Heartwood network upgrade on testnet.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This release does <strong><em>not</em></strong> support activation of Heartwood on mainnet. In order to follow the Heartwood upgrade on mainnet you will still need to upgrade to 3.0.0 (or a later version) when it is released in the coming month.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Heartwood network upgrade deploys <a href="https://zips.z.cash/zip-0213" target="_blank" rel="noreferrer noopener">ZIP 213</a>, which allows miners to <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/mine-to-shielded-coinbase/">mine directly into shielded addresses</a>. It also deploys <a href="https://zips.z.cash/zip-0221" target="_blank" rel="noreferrer noopener">ZIP 221</a>, enabling <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/explaining-flyclient/">Flyclient support</a> by changing the semantics of existing block header fields. The deployment process for the Heartwood upgrade is described in <a href="https://zips.z.cash/zip-0250" target="_blank" rel="noreferrer noopener">ZIP 250</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Testnet: Mining to Sapling addresses</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>After the activation of Heartwood on testnet, miners will be able to immediately shield funds to Sapling addresses in the coinbase transactions which mint new testnet coins (TAZ).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This release provides the ability for miners to specify <code>mineraddress=SAPLING_ADDRESS</code> in their <code>zcash.conf</code> file, where <code>SAPLING_ADDRESS</code> is a Sapling payment address that they can obtain using <code>z_getnewaddress</code>. However, miners should wait until Heartwood has activated on testnet before making this change to their configuration file, or else <code>getblocktemplate</code> will return block templates that cannot be mined.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sapling viewing key support</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release provides support for Sapling viewing keys (specifically, the extended viewing keys described in <a href="https://zips.z.cash/zip-0032" target="_blank" rel="noreferrer noopener">ZIP 32</a>) in the wallet. Nodes will track both sent and received transactions for any Sapling addresses associated with the Sapling viewing keys that have been imported into the wallet.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Use the <code>z_exportviewingkey</code> RPC method to obtain the viewing key for a shielded address in a node's wallet. For Sapling addresses, these always begin with "zxviews" (or "zxviewtestsapling" for testnet addresses).</li><li>Use <code>z_importviewingkey</code> to import a viewing key into another node. Imported Sapling viewing keys will be stored in the wallet, and remembered across restarts.</li><li><code>z_getbalance</code> will show the balance of a Sapling address associated with an imported Sapling viewing key. Balances for Sapling viewing keys will be included in the output of <code>z_gettotalbalance</code> when the <code>includeWatchonly</code> parameter is set to <code>true</code>.</li><li>RPC methods for viewing shielded transaction information (such as <code>z_listreceivedbyaddress</code>) will return information for Sapling addresses associated with imported Sapling viewing keys.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Details about what information can be viewed with these Sapling viewing keys, and what guarantees you have about that information, can be found in<a href="https://zips.z.cash/zip-0310" target="_blank" rel="noreferrer noopener"> ZIP 310</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>View shielded information in wallet transactions</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release introduces the <code>z_viewtransaction</code> RPC command. This command, given a transaction ID, will decrypt the transaction with all Sapling keys in the local wallet and return the shielded information that it can recover, including</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>The address that each note belongs to</li><li>Values in both decimal ZEC/TAZ and zatoshis</li><li>The ID of the transaction that each spent note was received in</li><li>An <code>outgoing</code> flag on each new note, which will be <code>true</code> if the output is not for an address in the wallet</li><li>A <code>memoStr</code> field for each new note, containing its text memo (if its memo field contains a valid UTF-8 string)</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Other changes</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>The <code>-maxtimeadjustment</code> option has been removed; node operators should ensure their node’s local time is configured properly.</li><li>Error messages for transactions that are rejected during network upgrades are more clear.</li><li>We’ve introduced a <code>-txexpirynotify</code> option which, similar to the <code>-blocknotify</code> config option, will perform the configured command whenever a transaction expires in the mempool.</li><li>The <code>z_importkey</code> and <code>z_importviewingkey</code> RPC methods now return the type of the imported spending or viewing key (Sprout or Sapling) and the corresponding payment address.</li><li>Negative heights are now permitted in <code>getblock</code> and <code>getblockhash</code>, to select blocks backwards from the chain tip. A height of <code>-1</code> corresponds to the last known valid block on the main chain.</li><li>A new RPC method <code>getexperimentalfeatures</code> returns the list of enabled experimental features.</li></ul>
<!-- /wp:list -->

<!-- wp:html -->
<div class="wp-block-spacer" style="height: 31px;" aria-hidden="true">&nbsp;</div>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>More details about the changes in this release can be found in the <a href="https://github.com/zcash/zcash/blob/master/doc/release-notes/release-notes-2.1.2.md" target="_blank" rel="noreferrer noopener">release notes</a>.</p>
<!-- /wp:paragraph -->