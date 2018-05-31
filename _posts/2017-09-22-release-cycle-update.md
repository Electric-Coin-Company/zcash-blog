---
ID: 1614
post_title: Release Cycle Update
author: Paige Peterson
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/release-cycle-update/
published: true
post_date: 2017-09-22 00:00:00
---
*Edit 2018-05-31:* Auto-senescence terminology changed to "end-of-support halt".

Ahead of the 1.0.9 release a few months ago, the Zcash development team <a class="reference external" href="/release-cycle-and-lifetimes/">announced</a> a new monthly release cycle and deprecation policy. We learned a lot in the first month of the release cycle and decided to extend it to 6 weeks. We've discussed this openly in the <a class="reference external" href="https://chat.zcashcommunity.com">community chat</a> <cite>#zcash-dev</cite> channel and in the weekly <a class="reference external" href="https://forum.z.cash/c/dev-updates">forum developer updates</a>.

This cycle extension allows for several improvements:
<ul class="simple">
 	<li>better planning of in-progress and subsequent releases;</li>
 	<li>more time for pre-release testing and development infrastructure improvements;</li>
 	<li>less frequent updating for users and third-party services.</li>
</ul>
<div id="auto-senescence-1-0-9-deprecation" class="section">
<h2>End-of-support halt &amp; 1.0.9 Deprecation</h2>
This change to the release cycle length affects how they line up with the end-of-support halt feature (previously called "auto-senescence") we introduced in the 1.0.9 update and the 18 week schedule it runs on. We do not plan on updating the deprecation time frame so now a version will become deprecated at about the same time the 3rd subsequent version is released. For example, version 1.0.9 will be deprecated just as version 1.0.12 is released. A warning will appear for nodes running the official Zcash client about two weeks before the version they are running is set to become deprecated.

As we stated previously, once a version is deprecated via the end-of-support halt feature, nodes running that version will automatically exit when they detect they've reached their deprecation phase. This feature will always have the ability to opt-out but it's important to note that for deprecated releases, the only help the Zcash Company user support team promises is in upgrading to the latest release.

At block 193076, all nodes running version 1.0.9 which do not have the <cite>-disabledeprecation=1.0.9</cite> flag set to opt out of end-of-support halt will automatically shut down. These nodes should already be receiving a related message about the upcoming version deprecation.

Of course we recommend that instead of using the configuration to disable deprecation of 1.0.9 that node operators <a class="reference external" href="https://z.cash/download.html">update</a> to the most recent version of <cite>zcashd</cite> or another well-maintained implementation. Client and network security improvements are often addressed in releases so it's a good idea to always stay updated with the most recent version. If there is a particular reason why you cannot update or do not want to, please reach out to us in the <a class="reference external" href="https://chat.zcashcommunity.com">community chat</a> or by <a class="reference external" href="mailto:info@z.cash">email</a> so we can better understand your needs. We're also happy to answer any questions about the release cycle or deprecation policy and will communicate any future changes to these processes we deem beneficial.
