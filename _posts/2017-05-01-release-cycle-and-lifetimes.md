---
ID: 1613
post_title: Release Cycle and Lifetimes
author: Nathan Wilcox
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/release-cycle-and-lifetimes/
published: true
post_date: 2017-05-01 00:00:00
---
Starting in May the Zcash development effort will institute a new release policy. There are a few immediate take-aways for users:
<ul class="simple">
 	<li>We'll release monthly on the third Tuesday, starting with 1.0.9 on May 16th.</li>
 	<li>Each release starting with 1.0.9 will become deprecated 4 months after its release date. <a id="id1" class="footnote-reference" href="#id3">[1]</a></li>
 	<li>We may deprecate releases earlier than this schedule to mitigate security vulnerabilities.</li>
</ul>
This is an aggressive upgrade schedule and if it doesn't work for your case, <a class="reference external" href="https://z.cash/contact.html">we'd love to hear from you</a> as soon as possible. This is all you need to know as a user, and the rest of this post describes our rationale and some protocol upgrade details.
<div id="better-safety-and-quality" class="section">
<h2>Better Safety and Quality</h2>
Since our launch we've used a tight three-week release schedule. We've shipped every release within a couple of days of the target date, with the exception of the last <a class="reference external" href="/zcash-1-0-9-postponed/">postponed 1.0.9 release</a> and an <a class="reference external" href="/new-release-1-0-8-1/">1.0.8-1 hotfix release</a>.

Our new process has slightly more time between releases. We'll use this extra time to add more thorough pre-release and package testing, have a retrospective meeting for each release, and begin per-release coordination for each of our longer term <a class="reference external" href="/the-near-future-of-zcash/">roadmap priorities</a>.

</div>
<div id="clearer-coordination" class="section">
<h2>Clearer Coordination</h2>
An essential change with this new policy is an explicit <cite>release lifecycle</cite>, the most important parts of which are the release date and the <cite>deprecation date</cite>, about four months later on the 4th third-Tuesday after the release.

For <cite>active releases</cite> which have not yet reached their deprecation date, we make our best effort to provide security fixes, follow up to bug reports, avoid disruption on the production network, and help users to upgrade to the latest release. For <cite>deprecated releases</cite> the only help we promise is in upgrading to the latest release.

In order to codify this cycle, we even intend to introduce a feature called <cite>auto-senescence</cite> starting in 1.0.9 which will cause nodes to automatically exit when they detect they've reached their deprecation phase. This feature will always have an opt-out, since (as discussed below) our goal is to give users their own choice, not to coerce or control them.

An important side-note: this policy is defined entirely in the context of a single release, so a user does not need to know anything about our future releases or our new policies for those releases in order to understand this policy for their own installation.
<div id="user-autonomy-deprecation-vs-auto-upgrade" class="section">
<h3>User autonomy: deprecation vs auto-upgrade</h3>
We consider user choice to be a paramount value to protect. Although this may sound abstract or overly dramatic it directly affects our technical design choices and plays out as our choice of a <cite>deprecation</cite> approach, rather than an <cite>auto-upgrade</cite> approach.

Auto-upgrade of apps has become widespread, because of numerous advantages. One of the most important advantages is in ensuring old software is rare so that vulnerabilities and technical debt are removed from the network thus making the whole safer.

Meanwhile, most users rely on default behavior, and a default auto-upgrade puts them de facto under the influence of a sole group of application developers. Most people believe this is fine, and while it often has been, we believe we're seeing a deep shift in de-facto governance due to these kinds of technological developments.

We prefer deprecation rather than auto-upgrade, where users must <em>themselves</em> choose either to upgrade to <em>our</em> new releases or <em>other people's</em> alternatives. We believe this still gives the systemic advantage of removing old software, yet users must explicitly opt-in to each upgrade, and each time is an opportunity to educate themselves and decide on a different fate.

</div>
<div id="how-is-deprecation-better-for-zcash" class="section">
<h3>How is deprecation better for Zcash?</h3>
Because users and our development community have this agreement, we can begin relying on this schedule for protocol upgrades, security fixes, usability improvements, and removing technical debt.

Once this policy is put in to place starting with our 1.0.9 release in May, we are on track to begin the protocol upgrade to the <a class="reference external" href="/the-near-future-of-zcash/">Sapling feature set</a>.

We'll also be able to roll out usability improvements, such as <cite>payment disclosure</cite> and in several months' time we'll know that support for those improvements <em>should be</em> widespread, and therefore all wallets and vendors will benefit from ecosystem-wide consistency.

I emphasized "should be" because users may always choose to reject our deprecation policy by editing their local configuration or installing alternative implementations. In that case, we'll have a clear signal from the user community about their reservations with our direction, so this is one of the key mechanisms of our improving governance.
<div id="id2" class="section">
<h4>We'd Love to Hear From You</h4>
Please reach out to us with any feedback on this new release policy. You can find us on the <a class="reference external" href="https://chat.zcashcommunity.com">community chat</a> or if preferred, reach out directly via <a class="reference external" href="mailto:info@z.cash">email</a>.
<table id="id3" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="#id1">[1]</a></td>
<td>We're still determining when and how to deprecate releases before 1.0.9.</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>