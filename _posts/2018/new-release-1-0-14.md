---
ID: 4990
post_title: 'New Release: 1.0.14'
post_name: new-release-1-0-14
post_date: 2018-01-04 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-1-0-14/
published: true
tags:
  - bugs
  - releases
  - sprout
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.14, which contains new features, bug fixes, and documentation improvements.</p>
<h2>Notable changes</h2>
<h3>Incoming viewing keys</h3>
<p>Support for incoming viewing keys, as described in <a class="reference external" href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">the Zcash protocol spec</a>, has been added to the wallet.</p>
<p>Use the <tt class="docutils literal">z_exportviewingkey</tt> RPC method to obtain the incoming viewing key for a z-address in a node's wallet. For Sprout z-addresses, these always begin with "ZiVK" (or "ZiVt" for testnet z-addresses). Use <tt class="docutils literal">z_importviewingkey</tt> to import these into another node.</p>
<p>A node that possesses an incoming viewing key for a z-address can view all past<br />
transactions received by that address, as well as all future transactions sent<br />
to it, by using <tt class="docutils literal">z_listreceivedbyaddress</tt>. They cannot spend any funds from the<br />
address. This is similar to the behaviour of "watch-only" t-addresses.</p>
<p><tt class="docutils literal">z_gettotalbalance</tt> now has an additional boolean parameter for including the<br />
balance of "watch-only" addresses (both transparent and shielded), which is set<br />
to <tt class="docutils literal">false</tt> by default. <tt class="docutils literal">z_getbalance</tt> has also been updated to work with<br />
watch-only addresses.</p>
<ul class="simple">
<li><strong>Caution:</strong> for z-addresses, these balances will <strong>not</strong> be accurate if any<br />
funds have been sent from the address. This is because incoming viewing keys<br />
cannot detect spends, and so the "balance" is just the sum of all received<br />
notes, including ones that have been spent. Some future use-cases for incoming<br />
viewing keys will include synchronization data to keep their balances accurate<br />
(e.g. <a class="reference external" href="https://github.com/zcash/zcash/issues/2542">#2542</a>).</li>
</ul>
<h3>Sprout circuit value tracking</h3>
<p>Nodes can now track the total amount of shielded ZEC inside the Sprout circuit.<br />
This is measured by adding up the ZEC moving between the Transparent Value Pool<br />
and JoinSplits (see <a class="reference external" href="/blog/anatomy-of-zcash/">Anatomy of a Zcash Transaction</a>).<br />
<tt class="docutils literal">getblockchaininfo</tt> shows the total for the entire chain, while <tt class="docutils literal">getblock</tt><br />
will show the total as of a specific block.</p>
<p>To enable this monitoring on a specific node, it must be re-indexed. This will<br />
take several hours to complete, but otherwise will not affect any other node<br />
data.</p>
<h2>Summary of the changes included in this release</h2>
<ol class="arabic simple">
<li>We fixed a non-exploitable buffer overflow in libsnark. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2800">#2800</a>)</li>
<li>We added support for incoming viewing keys. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2143">#2143</a>)</li>
<li>We added tracking of the total shielded value inside the Sprout circuit, which can be enabled by re-indexing. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2795">#2795</a>)</li>
<li>We modified <tt class="docutils literal">dumpwallet</tt> and <tt class="docutils literal">z_exportwallet</tt> to prevent them overwriting existing files. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2741">#2741</a>)</li>
<li>We fixed bugs on several unsupported platforms. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2700">#2700</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2752">#2752</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2786">#2786</a>)</li>
<li>We improved various parts of the help text and documentation. (<a class="reference external" href="https://github.com/zcash/zcash/pull/2724">#2724</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/2744">#2744</a>)</li>
</ol>
<p>We're encouraging all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a><br />
page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/64?closed=1">1.0.14</a><br />
GitHub milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a><br />
and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
