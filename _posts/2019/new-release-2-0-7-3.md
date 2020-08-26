---
ID: 8777
post_title: 'New Release: 2.0.7-3'
post_name: new-release-2-0-7-3
post_date: 2019-10-02 16:10:20
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-7-3/
published: true
tags:
  - releases
  - security
  - Security Announcement
categories:
  - General
---
<!-- wp:paragraph -->
<p>On Tuesday September 24th we released version 2.0.7-3 of Zcashd to address two security issues. Both were discovered and reported to us by Florian Tramèr, Dan Boneh, and Kenneth G. Paterson. The “REJECT” vulnerability was reported to us on Friday September 13th 2019, and the “PING” vulnerability was reported to us on Friday September 20th 2019. Their write-up is <a href="https://crypto.stanford.edu/timings/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">available online</a>. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Prior to this version, an attacker could have confirmed that they correctly knew that a given zcashd node was associated with an attacker-known shielded payment address by leveraging network connectivity to the target zcashd node.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Both vulnerabilities provided oracles to an adversary that allowed them to query the node to discover if it had authority over an attacker-known shielded payment address.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Issue Details</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The first issue (aka “REJECT”, which was later assigned CVE-2019-16930) affects only Sapling addresses, and is caused by an unhandled exception in the wallet processing code that results in a difference in the data within the reply to the peer submitting a transaction depending on whether the receiving peer has the viewing key loaded in the internal wallet or not. We fixed this in Zcashd 2.0.7-3 by changing the code to handle the exception. If an attacker’s attempt to exploit CVE-2019-16930 is mined and enters the blockchain, the victim’s (unfixed) node will crash upon receiving the block containing the attacker’s transaction. We are not aware of any reports of users’ nodes crashing in this way.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The second issue (aka “PING”, which was later assigned CVE-2019-17048), affects both Sapling and Sprout addresses, and is caused by the internal wallet code processing new transactions inline with the network code. An attacker could also forward a transaction from another node to the victim and learn the association between that transaction and the node without knowing the address. The timing of the victim node’s response to the attacker’s probing transaction is enough for the attacker to determine if the victim peer has the viewing key loaded. We fixed this in Zcashd 2.0.7-3 by changing the code to defer wallet processing of new transactions to another thread.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Indicators of Compromise</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>An attacker exploiting the REJECT vulnerability requires an active attack which will leave entries in the victim node’s debug.log file that looks like:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><code>EXCEPTION: std::ios_base::failure<br>lead byte of SaplingNotePlaintext is not recognized<br>Zcash in ProcessMessages()</code></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Logfile shrinking was disabled in 2.0.7-3 so as to collect evidence of an attempt of privacy compromise using these bugs.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Remediation</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Both issues were investigated thoroughly and fixed in version 2.0.7-3 of Zcashd which is the current stable release and was packaged and made available for download on September 25th.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We strongly advise users who have not yet upgraded to do so now through their usual update channels.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The update was announced on our security information <a href="https://z.cash/support/security/announcements/security-announcement-2019-09-24/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">page</a>. We recommend that users looking for the latest security news from Electric Coin Company monitor our <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://z.cash/support/security/announcements/" target="_blank">security announcements page</a>. </p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Acknowledgements</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We are extremely grateful to Florian Tramèr, Dan Boneh, and Kenneth G. Paterson for notifying and working with us in order to protect users.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We are extremely grateful to the organizations with whom we have bilateral vulnerability sharing agreements, in this case Komodo and Horizen.</p>
<!-- /wp:paragraph -->