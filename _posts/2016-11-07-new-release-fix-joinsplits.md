---
ID: 1603
post_title: 'New Release: 1.0.2'
author: Nathan Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/new-release-fix-joinsplits/
published: true
post_date: 2016-11-07 00:00:00
---
<p>Today we're announcing the release of Zcash 1.0.2 which fixes a bug that prevented creating transactions to multiple shielded recipient addresses. This is an implementation bug in the <tt class="docutils literal">zcashd</tt> wallet which does not impact the consensus protocol.</p>
<p>The list of changes included in this release:</p>
<ol class="arabic simple"><li>We fixed a bug to ensure that JoinSplit transactions to multiple z-addresses will succeed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1790">#1790</a>)</li>
<li>We changed z_sendmany to check if the size of a transaction for a given number of outputs will be valid. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1808">#1808</a>)</li>
<li>We fixed a bug that could crash the miner when it was interrupted. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1778">#1778</a>)</li>
<li>Community contributors helped improve our documentation. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1765">#1765</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1763">#1763</a>)</li>
</ol><p>We're encouraging all users and miners to update to this new version. See our <a class="reference external" href="https://z.cash/download.html">download</a> page and the <a class="reference external" href="https://github.com/zcash/zcash/wiki/1.0-User-Guide">1.0 User Guide</a> for more information.</p>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/45?closed=1">1.0.2</a> github milestone. To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>.</p>
<div class="section" id="background">
<h2>Background</h2>
<p>JoinSplits encapsulate zero-knowledge value transfer and have two private inputs and two private outputs. Multiple JoinSplits may be <cite>chained</cite> into a single transaction in order to spend more than two private inputs and/or send to more than two private outputs. The order of inputs and outputs can be a subtle information leak to private recipients (see <a class="reference external" href="https://github.com/zcash/zcash/issues/778">#778</a>). A patch to fix this information leak (<a class="reference external" href="https://github.com/zcash/zcash/pull/1561">#1561</a>) in our <a class="reference external" href="/new-release-candidate-less-than-one-week/">1.0.0-rc2</a> release randomizes the input and output orderings, but in doing so failed to permute the necessary commitment witnesses in the same manner as the private inputs. In this release we’ve temporarily disabled input/output order randomization (<a class="reference external" href="https://github.com/zcash/zcash/pull/1790">#1790</a>).</p>