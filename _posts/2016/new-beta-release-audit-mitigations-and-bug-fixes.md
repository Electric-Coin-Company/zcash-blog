---
ID: 4906
post_title: 'New Beta Release: Audit Mitigations and Bug Fixes'
post_name: >
  new-beta-release-audit-mitigations-and-bug-fixes
post_date: 2016-10-04 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-beta-release-audit-mitigations-and-bug-fixes/
published: true
tags:
  - beta
  - releases
categories:
  - General
---
<p>Today, we deployed the second beta release of the <a class="reference external" href="https://github.com/zcash">Zcash</a> reference implementation, <cite>1.0.0-beta2</cite>, to the testnet. This is the second release of the Zcash Beta Series. The new release includes the following changes <a class="footnote-reference" href="#id2" id="id1">[1]</a>:</p>
<ol class="arabic simple">
<li>We have changed the address prefixes. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1477">#1477</a>)</li>
<li>Encrypting your wallet with a passphrase now also encrypts the spending key for zaddrs. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1372">#1372</a>)</li>
<li>Founders’ Reward addresses will now rotate monthly. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1398">#1398</a>)</li>
<li>We have re-enabled disabled compiler warnings and updated all dependencies, including Boost and OpenSSL. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1429">#1429</a>)</li>
<li>We have merged in upstream patches to mitigate the risk of DoS attacks. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1411">#1411</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1407">#1407</a>)</li>
<li>We have deployed a dnsseed to improve launching and connecting to the network. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1443">#1443</a>)</li>
<li>The RPC call getbalance now returns a correct balance for UTXOs. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1427">#1427</a>)</li>
<li>High-priority alerts now put the RPC into safe mode. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1374">#1374</a>)</li>
<li>We have updated the public parameters. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1476">#1476</a>)</li>
</ol>
<p>This release also makes reliability improvements in the wallet, however some work remains to be done around importing keys and rescanning after restarts. If you are encountering problems with the wallet, stop your node and restart it with the <cite>-reindex</cite> flag (Example: <cite>./src/zcashd -reindex</cite>).</p>
<p>This release will reset our testnet, invalidating all previous coins and breaking backwards compatibility. To get connected to the new testnet, follow the instructions on the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Beta-Guide">Beta Guide</a>.</p>
<p>Additionally, you can now reach our main test network node through a Tor hidden service at <cite>zctestseie6wxgio.onion</cite>.</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
<table class="docutils footnote" frame="void" id="id2" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>For more specific detail, view our <a class="reference external" href="https://github.com/zcash/zcash/milestone/37">1.0.0-beta2</a> release github milestone.</td>
</tr>
</tbody>
</table>
