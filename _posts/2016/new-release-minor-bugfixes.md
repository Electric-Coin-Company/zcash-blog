---
ID: 4925
post_title: 'New Release: 1.0.1'
post_name: new-release-minor-bugfixes
post_date: 2016-11-03 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/new-release-minor-bugfixes/
published: true
tags:
  - bugs
  - releases
  - sprout
categories:
  - General
---
<p>Today we're announcing the release of Zcash 1.0.1, which fixes a few bugs and improves diagnostics:</p>
<ol class="arabic simple">
<li>Fixed a bug where transactions that contain shielded payments were not being mined in some circumstances. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1718">#1718</a>)</li>
<li>Invalid arguments passed when building JoinSplits now produce more descriptive errors. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1752">#1752</a>)</li>
<li>Added new RPC call, z_validateaddress (<a class="reference external" href="https://github.com/zcash/zcash/pull/1748">#1748</a>)</li>
<li>The friendly metrics screen has improved accuracy and additional information. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1735">#1735</a>)</li>
<li>A consensus rule improperly applied to the genesis block was adjusted. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1754">#1754</a>)</li>
<li><cite>fetch-params.sh</cite> has been improved and is included in the gitian build. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1758">#1758</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1759">#1759</a>)</li>
<li>A checkpoint was added for block 2500. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1750">#1750</a>)</li>
</ol>
<p>We're encouraging all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a> page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/45?closed=1">1.0.1</a> github milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
