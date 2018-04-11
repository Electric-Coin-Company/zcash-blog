---
ID: 1617
post_title: Security Announcement 2016-11-22
author: Nathan Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/security-announcement-2016-11-22/
published: true
post_date: 2016-11-22 00:00:00
---
<strong>Synopsis:</strong> A cache invalidation bug may allow an attacker to trigger a chain fork causing pre-1.0.3 nodes to follow an invalid chain. A fix is implemented in <a class="reference external" href="https://z.cash/download.html">zcashd release 1.0.3</a>.

ZcashCo, and several exchanges, wallet vendors, and miners have already deployed a mitigation as well as detectors for this attack vector. No attacks have been detected.

<strong>Who is at Risk:</strong> Users are at risk only when two conditions are met simultaneously:
<ol class="arabic simple">
 	<li>They rely on <a class="reference external" href="https://github.com/zcash/zcash/releases">zcashd releases</a> older than 1.0.3, including 1.0.0, 1.0.1, and 1.0.2, <em>AND</em></li>
 	<li>A network-wide attack is executed to trigger a chain fork. This requires a majority of miners to run vulnerable software.</li>
</ol>
Users who rely on third party services should inquire if those services have mitigated this issue. We have collaborated with major exchanges, wallet providers, and miners and they have already mitigated this issue for their services.

<strong>Who is not at Risk:</strong> Users who meet <em>either</em> of the following two conditions are not at risk:
<ol class="arabic simple">
 	<li>they have upgraded to <cite>zcashd 1.0.3</cite>, or rely on a service which has done so, <em>OR</em></li>
 	<li>no network-wide attack has succeeded (for example, because a sufficient portion of miners have mitigated the vulnerability).</li>
</ol>
In other words: individuals and services are protected as soon as they upgrade, and the entire network is protected as soon as a sufficient portion of miners upgrade.

<strong>How can at-risk users protect themselves?</strong>
<ol class="arabic simple">
 	<li>Upgrading to <a class="reference external" href="https://z.cash/download.html">zcashd release 1.0.3</a> is the most certain protection.</li>
 	<li>For users of third party services (such as exchanges, wallets, or mining pools), check if the service has announced upgrading to <cite>zcashd 1.0.3</cite>. If it hasn't, consider pausing use of that service until they announce an upgrade.</li>
</ol>
<strong>How can I tell if an attack is occurring?</strong> ZcashCo and several large exchanges, wallet providers, and miners have deployed sensors which detect attacks against this vector. In the event that an attack is detected, the ZcashCo will take the following actions:
<ul>
 	<li>
<p class="first">The Zcash developers will issue an in-band alert, causing all <cite>zcashd</cite> nodes to announce the potential attack.</p>
</li>
 	<li>
<p class="first">ZcashCo will always announce known ongoing attacks in these places:</p>

<blockquote>
<ul class="simple">
 	<li>a banner on every page of this website,</li>
 	<li>the <a class="reference external" href="https://z.cash/support/security.html">security notifications</a> page of this website,</li>
 	<li>the <a class="reference external" href="https://twitter.com/zcashco">@ZcashCo</a> twitter stream,</li>
 	<li>the <a class="reference external" href="https://chat.zcashcommunity.com/channel/zcash">#zcash community chat room</a>, <em>and</em></li>
 	<li>the <a class="reference external" href="https://forum.z.cash/">Zcash forum</a>.</li>
</ul>
</blockquote>
</li>
 	<li>
<p class="first">ZcashCo will coordinate in private channels with major exchanges, wallet vendors, and mining outfits to alert them of the attack and to post their own announcements.</p>
</li>
</ul>
<em>Note:</em> The major exchanges, wallet vendors, and miners we are in communication with are already protected against such an attack.

<strong>Impact:</strong> <em>If</em> a network attack is successfully executed (which requires a majority of mining capacity to be vulnerable) then <em>only</em> users running vulnerable clients will follow a chain fork that is invalid. Transactions on that fork will be rolled back as more miners upgrade to the valid fork.

<strong>Technical Background:</strong> Due to a cache invalidation bug, some nodes on the Zcash network will accept particular invalid transactions as valid <a id="id1" class="footnote-reference" href="/security-announcement-2016-11-22#id2">[1]</a>. If a majority of the network hashrate accepts an invalid transaction as valid, there could be a chain fork.

<strong>Followup Announcements:</strong>
<ul class="simple">
 	<li>See the <a class="reference external" href="https://z.cash/support/security.html">security notifications</a> page for further updates on this issue, and any future security issue.</li>
 	<li>Continue to check this blog.</li>
</ul>
<table id="id2" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="https://z.cash/blog/security-announcement-2016-11-22.html#id1">[1]</a></td>
<td>Note that transaction validity is well specified by our protocol specification, <a class="reference external" href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">Zcash protocol specification, v2016.0-beta-1.10</a>; It is unambiguous that this security flaw is an implementation bug.</td>
</tr>
</tbody>
</table>