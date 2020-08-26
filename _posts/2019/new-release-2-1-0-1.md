---
ID: 8919
post_title: 'New Release: 2.1.0-1'
post_name: new-release-2-1-0-1
post_date: 2019-11-08 18:38:21
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-1-0-1/
published: true
tags: [ ]
categories:
  - General
  - Technical
---
<!-- wp:spacer {"height":33} -->
<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:paragraph -->
<p>Electric Coin Co. became aware of the following security announcement on the bitcoin-dev mailing list this morning (8th November): <a href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-November/017453.html">https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-November/017453.html</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Upon investigation, the team found that versions of Zcashd prior to 2.1.0-1 suffered from the above bug, CVE-2017-18350. Nodes in the affected configuration could be compromised by an attacker executing arbitrary code in the context of the Zcashd daemon, allowing them to violate user privacy, steal user funds, or perform other unauthorized actions on the machine.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Zcashd version 2.1.0-1 contains a fix for this issue, and we recommend updating all affected nodes as soon as possible.</p>
<!-- /wp:paragraph -->