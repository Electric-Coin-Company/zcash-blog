---
ID: 5003
post_title: 'New Release: 1.1.0'
post_name: new-release-1-1-0
post_date: 2018-04-14 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-1-1-0/
published: true
tags:
  - bugs
  - Overwinter
  - releases
categories:
  - General
---
<p><strong>Edit 2018-05-31:</strong> Auto-senescence terminology changed to "end-of-support halt".</p>
<p>After several months of work, we are happy to announce the release of Zcash 1.1.0, the first Overwinter-compatible version of the Zcash node software!</p>
<h2>Overwinter network upgrade</h2>
<p>The first block of Overwinter will be block 347500, which is expected to be mined on the 25th of June 2018, just before noon EDT / 16:00 UTC. Please upgrade to this release, or any subsequent release, in order to follow the Overwinter network upgrade. See our <a href="/blog/overwinter/">previous blog post</a> and the <a href="https://z.cash/upgrade/overwinter.html">Overwinter Network Upgrade page</a> for more information.</p>
<h2>Other notable changes</h2>
<h3><code>-mempooltxinputlimit</code> deprecation</h3>
<p>The <code>-mempooltxinputlimit</code> configuration option was added in release 1.0.10 as a short-term fix for the quadratic hashing problem inherited from Bitcoin. At the time, transactions with many inputs were causing performance issues for miners. Since then, several performance improvements were merged from the Bitcoin Core codebase to significantly reduce these issues.</p>
<p>The Overwinter network upgrade includes changes that solve the quadratic hashing problem. As a result, the <code>-mempooltxinputlimit</code> option is no longer needed. A transaction with 1000 inputs will take just as long to validate as 10 transactions with 100 inputs each. Starting from this release, <code>-mempooltxinputlimit</code> will be enforced before the Overwinter activation height is reached, but will be ignored once Overwinter activates. The option will be removed entirely in a future release after Overwinter has activated.</p>
<h3><code>NODE_BLOOM</code> service bit</h3>
<p>Support for the <code>NODE_BLOOM</code> service bit, as described in <a href="https://github.com/bitcoin/bips/blob/master/bip-0111.mediawiki">BIP 111</a>, has been added to the P2P protocol code.</p>
<p>BIP 111 defines a service bit to allow peers to advertise that they support Bloom filters (such as used by SPV clients) explicitly. It also bumps the protocol version to allow peers to identify old nodes which allow Bloom filtering of the connection despite lacking the new service bit.</p>
<p>In this version, it is only enforced for peers that send protocol versions <code>&gt;=170004</code>. The plan is to remove this restriction in the next major version. Updating SPV clients to check for the <code>NODE_BLOOM</code> service bit for nodes that report version 170004 or newer is recommended.</p>
<h2>Summary of the changes included in this release</h2>
<ol>
<li>Set the Overwinter mainnet activation height. (<a href="https://github.com/zcash/zcash/pull/3165">#3165</a>)</li>
<li>Deprecated <code>-mempooltxinputlimit</code>. (<a href="https://github.com/zcash/zcash/pull/3098">#3098</a>)</li>
<li>Pulled in support for the <code>NODE_BLOOM</code> service bit. (<a href="https://github.com/zcash/zcash/pull/2814">#2814</a>)</li>
<li>Fixed a bug in the block index rewinding code added in 1.0.15. (<a href="https://github.com/zcash/zcash/pull/3132">#3132</a>, <a href="https://github.com/zcash/zcash/pull/3166">#3166</a>)</li>
<li>Fixed a bug in <code>z_mergetoaddress</code> when running it several times in parallel. (<a href="https://github.com/zcash/zcash/pull/3106">#3106</a>)</li>
<li>Fixed a bug where mainnet end-of-support halt (previously called "auto-senescence") heights were applied to testnet and regtest. (<a href="https://github.com/zcash/zcash/pull/3069">#3069</a>)</li>
<li>Fixed bugs on several unsupported platforms. (<a href="https://github.com/zcash/zcash/pull/2820">#2820</a>, <a href="https://github.com/zcash/zcash/pull/2965">#2965</a>, <a href="https://github.com/zcash/zcash/pull/3089">#3089</a>, <a href="https://github.com/zcash/zcash/pull/3117">#3117</a>)</li>
<li>Made Rust compilation mandatory. (<a href="https://github.com/zcash/zcash/pull/3127">#3127</a>)</li>
<li>Added support for Rust crates to the depends system. (<a href="https://github.com/zcash/zcash/pull/3096">#3096</a>)</li>
<li>Upgraded OpenSSL to 1.1.0h. (<a href="https://github.com/zcash/zcash/pull/3130">#3130</a>)</li>
<li>Improved the error message for "absurdly high fees". (<a href="https://github.com/zcash/zcash/pull/3111">#3111</a>)</li>
<li>Added logging of expired transactions. (<a href="https://github.com/zcash/zcash/pull/3090">#3090</a>)</li>
</ol>
<p>We’re encouraging all users and miners to update to this version. See the <a class="reference external" href="https://z.cash/download.html">download</a> page and <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see the <a href="https://github.com/zcash/zcash/milestone/70?closed=1">1.1.0</a> GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
