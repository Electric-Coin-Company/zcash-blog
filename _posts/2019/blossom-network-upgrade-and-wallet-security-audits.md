---
ID: 8262
post_title: >
  Blossom Network Upgrade and Wallet
  Security Audits
post_name: >
  blossom-network-upgrade-and-wallet-security-audits
post_date: 2019-07-19 15:56:46
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/blossom-network-upgrade-and-wallet-security-audits/
published: true
tags:
  - audit
  - security
  - security audits
categories:
  - General
---
<!-- wp:paragraph -->
<p>Three separate audit reports of Electric Coin Company software have been completed. The first two target the Zcash Improvement Proposals (ZIPs) for the Blossom network upgrade, scheduled for activation this fall. The other targets the mobile reference wallet SDK.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Blossom</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We engaged <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://coinspect.com/" target="_blank">Coinspect</a> and <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.nccgroup.trust/us/" target="_blank">NCC Group</a> to perform security assessments of the original ZIPs that formed the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://z.cash/upgrade/blossom/" target="_blank">Blossom (NU2) network upgrade</a>. The improvements under investigation were: “Split Founders' Reward” (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/blob/master/zip-0207.rst" target="_blank">ZIP 207</a>) and “Shorter Block Target Spacing” (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/blob/master/zip-0208.rst" target="_blank">ZIP 208</a>).<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We interpret from these reports that both vendors reached similar conclusions about the security of decreased block spacing. In Zcash, a transaction is currently considered finalized with 10 or more confirmations. These reports show that effective finality can be achieved with the same level of safety sooner for a given mined transaction but not with linear improvement. The decreased time to finality and network throughput would be improved by this change at the cost of increasing minimum system requirements to verify all transactions. This feature will progress to implementation.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Subsequent to this security audit, but based primarily on other factors, we have <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3673" target="_blank">decided</a> to drop support for ZIP 207 and not implement it in the Blossom upgrade, and we have no plans to implement it in the future.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For more details, see the full reports:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a rel="noreferrer noopener" aria-label="Coinspect (opens in a new tab)" href="https://drive.google.com/file/d/1RlCGnTzVetpWX00SxHmpTXIHHWZ30tR5/view?usp=sharing" target="_blank">Coinspect</a></li><li><a href="https://www.nccgroup.trust/contentassets/71330b3ddc544c8c91486aa3fb2d7510/ncc_group_zcash_blossomspec_report_2019-06-01_v1.01.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">NCC Group</a></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Mobile Wallet</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The reference wallet SDK architecture underwent a point-in-time external security assessment using the testing services of <a href="https://www.bishopfox.com/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Bishop Fox</a>. Since the reference wallet software is not yet ready for production use, the assessment was limited in time and scope to architectural issues and a brief implementation review.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The findings indicated that we needed better vulnerability detection in our upstream dependencies for the SDK, which has now been added. The connection between SDK and lightwalletd still needs encryption and authentication for production deployments.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The intended deployment of this software is such that integrators will likely need to figure out how to secure those connections for their production uses. To support ecosystem security, we will be pursuing research on some options to suggest to implementers.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For more details, see <a href="https://drive.google.com/file/d/1ColvwG3c6GCsGuWpNK2Yk5x39vlLy4wB/view?usp=sharing" target="_blank" rel="noreferrer noopener" aria-label="the full report (opens in a new tab)">the full report</a>.<br></p>
<!-- /wp:paragraph -->