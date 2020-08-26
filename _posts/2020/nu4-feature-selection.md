---
ID: 9637
post_title: NU4 feature selection
post_name: nu4-feature-selection
post_date: 2020-05-07 18:42:40
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/nu4-feature-selection/
published: true
tags:
  - Canopy
  - Dev Fund
  - network upgrade
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>As part of the Zcash Improvement Proposal and Network Upgrade Pipeline, Electric Coin Co. (ECC) is publishing our commitment of company resources to proposals for the Network Upgrade 4 (NU4), due to activate in November 2020. We reviewed these proposed features with the Zcash Foundation and reached agreement on the inclusion of the ZIPs outlined here, subject to the outcome of security audits.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>About feature selection</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The primary impetus for NU4 is to implement protocol and consensus-level changes related to the advent of the Zcash Development Fund (a.k.a. the Dev Fund) which is outlined in <a href="https://zips.z.cash/zip-1014" target="_blank" rel="noreferrer noopener">ZIP 1014</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For other ZIPs not related to the Dev Fund, ECC answered these questions:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Is the ZIP sufficiently specified, such that it could be successfully implemented in NU4?</li><li>Does the ZIP introduce an unacceptable level of risk or complexity given the criticality of successful implementation of the Dev Fund related ZIPs in NU4?</li><li>Do we believe the impact of the ZIP will be a net benefit for Zcash?&nbsp;</li><li>For those ZIPs that are sufficiently specified, that do not introduce an unacceptable level of risk, and which we approve of, which will ECC commit to designing, implementing, auditing, and testing, to deploy safely and on time for NU4?</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>There are some nuances to these answers, especially for Questions 2 and 3, which involves a lot of discretionary judgment. For example, a ZIP may be well specified, and we may approve of the general idea, yet a specific ZIP may have some detail that impacts use cases or tradeoffs in a way we find unacceptable or introduces a level of complexity we find too risky at the current time.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading -->
<h2>NU4 ZIPs that ECC will implement</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The following are proposals which we believe are well-specified, which do not introduce an unacceptable level of risk, which we judge to be a net benefit for Zcash, and to which ECC will commit our resources to deploying in NU4:</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":4} -->
<h4>Dev Fund ZIPs</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>ZIP 207 - Funding streams</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://zips.z.cash/zip-0207" target="_blank" rel="noreferrer noopener">[link]</a> This proposal specifies a mechanism to support funding streams, distributed from a portion of the block subsidy for a specified range of block heights. This is intended as a means of implementing the Zcash Development Fund, using the funding stream definitions specified in <a href="https://zips.z.cash/zip-0214" target="_blank" rel="noreferrer noopener">ZIP 214</a>. It should be read in conjunction with <a href="https://zips.z.cash/zip-1014" target="_blank" rel="noreferrer noopener">ZIP 1014</a>, which describes the high-level requirements for that fund.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ZIP 214 - Consensus rules for a Zcash development fund</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a rel="noreferrer noopener" href="https://zips.z.cash/zip-0214" target="_blank">[link]</a> This ZIP describes consensus rule changes interpreting the proposed structure of the Zcash Development Fund, which is to be enacted in Network Upgrade 4 and last for 4 years. An important motivation for describing the consensus rules in a separate ZIP is to avoid making unintended changes to <a href="https://zips.z.cash/zip-1014" target="_blank" rel="noreferrer noopener">ZIP 1014</a>, which has already been agreed upon by ECC, ZF and the Zcash community. This facilitates critically assessing whether the consensus rule changes accurately reflect the intent of <a href="https://zips.z.cash/zip-1014" target="_blank" rel="noreferrer noopener">ZIP 1014</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ZIP 251: Deployment of the ${NU4} Network Upgrade</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://zips.z.cash/zip-0251" target="_blank" rel="noreferrer noopener">[link]</a> This proposal defines the deployment of the ${NU4} network upgrade. Note that the network handshake and peer management mechanisms defined in <a href="https://zips.z.cash/zip-0201" target="_blank" rel="noreferrer noopener">ZIP 201</a> also apply to this upgrade.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":4} -->
<h4>Other ZIPs</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>ZIP 211 - Disabling addition of new value to the Sprout value pool</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a rel="noreferrer noopener" href="https://github.com/zcash/zips/pull/214" target="_blank">[link]</a> This would be a step in the process of ensuring that Sprout funds would migrate out of the Sprout shielded pool whenever the owners decided to move those funds.&nbsp; It prevents new funds from entering the Sprout pool by shielding transactions. It does not prevent transfers within the Sprout pool.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ZIP 212 - Transfer Sapling ephemeral secret to recipient in note plaintext</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://github.com/zcash/zips/pull/222" target="_blank" rel="noreferrer noopener">[link]</a> This protects against a subtle, theoretical privacy weakness related to the use of diversified addresses. This also fixes an obstacle in developing a comprehensive security argument for Zcash privacy properties. Specifically, the goal of this is to avoid an assumption on zk-SNARK knowledge soundness in order to prevent an interactive attack that could link together diversified addresses.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ZIP 215 - Fix Ed25519 validation rules to allow batch verification</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://github.com/zcash/zips/pull/355" target="_blank" rel="noreferrer noopener">[link]</a> Zcash uses Ed25519 signatures as part of Sprout transactions. However, Ed25519 does not clearly define criteria for signature validity, and RFC-conformant implementations need not agree on whether signatures are valid. This is unacceptable for a consensus-critical application like Zcash. Currently, Zcash inherits criteria for signature verification from an obsolete version of libsodium. Instead, this ZIP clears the situation by explicitly defining the Ed25519 verification criteria and changing them to be compatible with batch verification</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<div class="wp-block-spacer" style="height: 45px;" aria-hidden="true">&nbsp;</div>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>ECC is excited to see the Dev Fund era begin post NU4 and we look forward to collaborating with other developers and teams on future network upgrades. Finally, we’re learning and refining the network upgrade process through each cycle and look forward to working with the ecosystem to define a more agile process while retaining the safeguards that have provided several successful upgrades throughout the years. We’re excited about the future of Zcash and look forward to working with the community and major grant recipients on NU5!</p>
<!-- /wp:paragraph -->