---
ID: 1619
post_title: Security Announcement 2017-04-13
author: Zooko Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/security-announcement-2017-04-13/
published: true
post_date: 2017-04-13 00:00:00
---
<strong>Synopsis:</strong> A bug related to transaction priority handling may allow an attacker to crash Zcash nodes (DoS) via a specially crafted transaction. A fix is implemented in <a class="reference external" href="https://z.cash/download.html">zcashd release 1.0.8-1</a>.

There is a <a class="reference external" href="/new-release-1-0-8-1">separate release post</a> documenting the included changes.

ZcashCo, and several exchanges, wallet vendors, and miners have already deployed a mitigation as well as detectors for this attack vector. No attacks have been detected.

<strong>Who is at Risk:</strong> Users are at risk who rely on <a class="reference external" href="https://github.com/zcash/zcash/releases">zcashd releases</a> starting with 1.0.4 up to and including 1.0.8.

We have collaborated with major exchanges, wallet providers, and miners and they have already mitigated this issue for their services.

<strong>Who is not at Risk:</strong> Users who have upgraded to <cite>zcashd 1.0.8-1</cite>, or rely on a service which has done so are not at risk.

<strong>How can at-risk users protect themselves?</strong>
<ol class="arabic simple">
 	<li>Upgrading to <a class="reference external" href="https://z.cash/download.html">zcashd release 1.0.8-1</a> is the most certain protection.</li>
 	<li>For users of third party services (such as exchanges, wallets, or mining pools), check if the service has announced upgrading to <cite>zcashd 1.0.8-1</cite>.</li>
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

<strong>Impact:</strong> <em>If</em> an attack transaction is successfully executed then <em>only</em> the users running vulnerable clients which have accepted the transaction in their mempool will be vulnerable. Accepting an attacker's transaction with an old client may cause the Zcash client to crash.

<strong>Technical Background:</strong> Zcash, like Bitcoin, assigns a priority to transactions in order to decide whether they should be accepted into a node's mempool. In practice the current transaction volume for Zcash is sufficiently low that this rarely has an effect, but the mechanism is still enabled. In Zcash 1.0.4, a change was made to this calculation to boost the priority of shielded transactions. However, an error in this code can –in circumstances that are normally rare, but can be forced by an attacker– result in an out-of-bounds memory access, which causes a segmentation fault.

<strong>Followup Announcements:</strong>
<ul class="simple">
 	<li>See the <a class="reference external" href="https://z.cash/support/security.html">security notifications</a> page for further updates on this issue, and any future security issue.</li>
 	<li>Continue to check this blog.</li>
</ul>
<strong>Acknowledgements</strong>

The Zcash Company would like to thank Juliano Rizzo from Coinspect and @movcrx from the Zclassic project for collaborating with us in analyzing and mitigating this issue.