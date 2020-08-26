---
ID: 8862
post_title: 'New Release: 2.1.0'
post_name: new-release-2-1-0
post_date: 2019-11-07 19:24:38
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-1-0/
published: true
tags:
  - network upgrade
  - releases
categories:
  - General
---
<!-- wp:heading -->
<h2>Blossom network upgrade</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The mainnet activation of the Blossom network upgrade is supported by this release, with an activation height of 653600, which should occur in early December, roughly one day following the targeted EOS halt of our 2.0.7-3 release. Please upgrade to this release, or any subsequent release, in order to follow the Blossom network upgrade.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Blossom network upgrade implements <a href="https://zips.z.cash/zip-0208">ZIP 208</a>, which shortens block times from 150s to 75s.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>DoS mitigation: Mempool size limit and random drop</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This release adds a mechanism for preventing nodes from running out of memory in the situation where an attacker is trying to overwhelm the network with transactions. This is achieved by keeping track of and limiting the total <code>cost</code> and <code>evictionWeight</code> of all transactions in the mempool. The <code>cost</code> of a transaction is determined by its size in bytes, and its <code>evictionWeight</code> is a function of the transaction's <code>cost</code> and its fee. The maximum total cost is configurable via the parameter <code>mempooltxcostlimit</code> which defaults to 80,000,000 (up to 20,000 txs). If a node's total mempool <code>cost</code> exceeds this limit, the node will evict a random transaction, preferentially picking larger transactions and ones with below-the-standard fees. To prevent a node from re-accepting evicted transactions, it keeps track of ones that it has evicted recently. By default, a transaction will be considered recently evicted for 60 minutes, but this can be configured with the parameter <code>mempoolevictionmemoryminutes</code>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For full details see&nbsp;<a href="https://github.com/zcash/zips/pull/275">ZIP 401</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Asynchronous operations incorrectly reporting success</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We fixed an issue where asynchronous operations were sometimes reporting success when they had actually failed. One way this could occur was when trying to use <code>z_sendmany</code> to create a transaction spending Coinbase funds in a way where change would be generated (not a valid use of <code>z_sendmany</code>). In this case, the operation would erroneously report success, and the only way to see that the transaction had actually failed was to look in the <code>debug.log</code> file. Such operations will now correctly report that they have failed.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Fake chain detection during initial block download</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>One of the mechanisms that&nbsp;<code>zcashd</code>&nbsp;uses to detect whether it is in "initial block download" (IBD) mode is to compare the active chain's cumulative work against a hard-coded "minimum chain work" value. This mechanism (inherited from Bitcoin Core) means that once a node exits IBD mode, it is either on the main chain, or a fake alternate chain with similar amounts of work. In the latter case, the node has most likely become the victim of a 50% + 1 adversary.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Starting from this release, <code>zcashd</code> additionally hard-codes the block hashes for the activation blocks of each past network upgrade (NU). During initial chain synchronization, and after the active chain has reached "minimum chain work," the node checks the blocks at each NU activation height against the hard-coded hashes. If any of them do not match, the node will immediately alert the user and <strong>shut down for safety</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Disabling old Sprout proofs</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As part of our ongoing work to clean up the codebase and minimize the security surface of <code>zcashd</code>, we are removing <code>libsnark</code> from the codebase and dropping support for creating and verifying old Sprout proofs. Funds stored in Sprout addresses are not affected, as they are spent using the hybrid Sprout circuit (built using <code>bellman</code>) that was deployed during the Sapling network upgrade.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This change has several implications:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><code>zcashd</code> no longer verifies old Sprout proofs and will instead assume they are valid. This has a minor implication for nodes: During initial block download, an adversary could feed the node fake blocks containing invalid old Sprout proofs, and the node would accept the fake chain as valid. However, as soon as the active chain contains at least as much work as the hard-coded "minimum chain work" value, the node will detect this situation and shut down.</li><li>Shielded transactions can no longer be created before Sapling has activated. This does not affect Zcash itself, but it will affect downstream codebases that have not yet activated Sapling (or that start a new chain after this point and do not activate Sapling from launch). Note that the old Sprout circuit is <a href="https://z.cash/support/security/announcements/security-announcement-2019-02-05-cve-2019-7167/">vulnerable to counterfeiting</a> and should not be used in current deployments.</li><li>Starting from this release, the circuit parameters from the original Sprout MPC are no longer required to start <code>zcashd</code>, and will not be downloaded by <code>fetch-params.sh</code>. They are not being automatically deleted at this time.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>We would like to take a moment to thank the&nbsp;<code>libsnark</code>&nbsp;authors and contributors. It was vital to the success of Zcash, and the development of zero-knowledge proofs in general, to have this code available and usable.</p>
<!-- /wp:paragraph -->