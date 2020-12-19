---
ID: 10136
post_title: New Release 3.1.0
post_name: new-release-3-1-0
post_date: 2020-07-30 21:16:05
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-3-1-0/
published: true
tags:
  - network upgrade
categories:
  - Technical
---
<!-- wp:heading -->
<h2>Network Upgrade 4: Canopy</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The code preparations for the Canopy network upgrade are finished and included in this release. The following ZIPs are being deployed:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://zips.z.cash/zip-0207" target="_blank" aria-label="undefined (opens in a new tab)" rel="noreferrer noopener">ZIP 207: Funding Streams</a></li><li><a href="https://zips.z.cash/zip-0211" target="_blank" aria-label="undefined (opens in a new tab)" rel="noreferrer noopener">ZIP 211: Disabling Addition of New Value to the Sprout Value Pool</a></li><li><a href="https://zips.z.cash/zip-0212" target="_blank" aria-label="undefined (opens in a new tab)" rel="noreferrer noopener">ZIP 212: Allow Recipient to Derive Sapling Ephemeral Secret from Note Plaintext</a></li><li><a href="https://zips.z.cash/zip-0214" target="_blank" aria-label="undefined (opens in a new tab)" rel="noreferrer noopener">ZIP 214: Consensus rules for a Zcash Development Fund</a></li><li><a href="https://zips.z.cash/zip-0215" target="_blank" aria-label="undefined (opens in a new tab)" rel="noreferrer noopener">ZIP 215: Explicitly Defining and Modifying Ed25519 Validation Rules</a></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Canopy will activate on testnet at height 1028500 (around August 5) and can also be activated at a specific height in regtest mode by setting the config option <code>-nuparams=0xe9ff75a6:HEIGHT</code>. Note that v3.1.0 enables Canopy support on the testnet.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Canopy will activate on mainnet at height 1046400 (mid-November).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>See <a aria-label="undefined (opens in a new tab)" href="https://zips.z.cash/zip-0251" target="_blank" rel="noreferrer noopener">ZIP 251</a> for additional information about the deployment process for Canopy.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Debian 8 "Jessie" will no longer be supported after v3.1.0, due to its <a aria-label="undefined (opens in a new tab)" href="https://www.debian.org/News/2020/20200709#:~:text=The%20Debian%20Long%20Term%20Support,security%20updates%20for%20Debian%208" target="_blank" rel="noreferrer noopener">end-of-life</a> on June 30, 2020. This will allow us to direct more resources to supporting Debian 10 Buster, other Linux distributions, and other platforms such as Windows and macOS.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Flush witness data to disk only when it's consistent</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This fix prevents the wallet database from getting into an inconsistent state. By flushing witness data to disk from the wallet thread, instead of the main thread, we ensure that the on-disk block height is always the same as the witness data height. Previously, the database occasionally got into a state where the latest block height was one ahead of the witness data. This then triggered an assertion failure in <code>CWallet::IncrementNoteWitnesses()</code> upon restarting after a zcashd shutdown.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Note that this code change will not automatically repair a data directory that has been affected by this problem; that requires starting zcashd with the <code>-rescan</code> or <code>-reindex</code> options.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>New DNS seeders</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>DNS seeders hosted at "zfnd.org" and "yolo.money" have been added to the list in <code>chainparams.cpp</code>. They're running <a aria-label="undefined (opens in a new tab)" href="https://coredns.io/" target="_blank" rel="noreferrer noopener">CoreDNS</a> with a <a aria-label="undefined (opens in a new tab)" href="https://github.com/ZcashFoundation/dnsseeder" target="_blank" rel="noreferrer noopener">Zcash crawler plugin</a>, the result of a Zcash Foundation in-house development effort to replace <code>zcash-seeder</code> with something memory-safe and easier to maintain. These are validly operated seeders per the <a aria-label="undefined (opens in a new tab)" href="https://zcash.readthedocs.io/en/latest/rtd_pages/dnsseed_policy.html" target="_blank" rel="noreferrer noopener">existing policy</a>. For general questions related to either seeder, contact george@zfnd.org or mention @gtank in the Zcash Foundation's Discord. For bug reports, open an issue on the <a aria-label="undefined (opens in a new tab)" href="https://github.com/ZcashFoundation/dnsseeder" target="_blank" rel="noreferrer noopener">dnsseeder</a> repo.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Changed command-line options</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><code>-debuglogfile=&lt;file&gt;</code> can be used to specify an alternative debug logging file.</li></ul>
<!-- /wp:list -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>RPC methods</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><code>joinSplitPubKey</code> and <code>joinSplitSig</code> have been added to verbose transaction outputs. This enables the transaction's binary form to be fully reconstructed from the RPC output.</li><li>The output of <code>getblockchaininfo</code> now includes an <code>estimatedheight</code> parameter. This can be shown in UIs as an indication of the current chain height while zcashd is syncing, but should not be relied upon when creating transactions.</li></ul>
<!-- /wp:list -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Metrics screen</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>A progress bar is now visible when in Initial Block Download mode, showing both the prefetched headers and validated blocks. It is only printed for TTY output. Additionally, the "not mining" message is no longer shown on mainnet, as the built-in CPU miner is not effective at the current network difficulty.</li><li>The number of block headers prefetched during Initial Block Download is now displayed alongside the number of validated blocks. With current compile-time defaults, a Zcash node prefetches up to 160 block headers per request without a limit on how far it can prefetch, but only up to 16 full blocks at a time.</li></ul>
<!-- /wp:list -->