---
ID: 8590
post_title: 'New Release: 2.0.7-2'
post_name: new-release-2-0-7-2
post_date: 2019-09-04 00:27:32
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-2-0-7-2/
published: true
tags:
  - Blossom
  - hotfix
  - releases
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>Testnet users needed to upgrade to 2.0.7 before Blossom activated. The amount of notice given to these users was brief, so many were not able to upgrade in time. These users may now be on the wrong branch. v2.0.7-2 adds an "intended rewind" to the Zcash testnet to prevent having to manually reindex when reconnecting to the correct chain. Also, an Insight Explorer related logging issue was also fixed, where <code>ERROR: spent index not enabled</code> was being logged unnecessarily.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Note</strong>: This release of Zcashd is a hotfix release following 2.0.7-1, which was merged and tagged with an incorrect end of support halt height, then removed. To avoid delaying the activation of mainnet blossom, we released a version 2.0.7-2 with the same end of support halt as 2.0.7, which is estimated to happen on 2019-12-10. The next release, v2.1.0, will support Blossom activation on mainnet which will happen a day later, estimated for 2019-12-11.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Summary of the Changes</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol>
<li><strong>Testnet Blossom "Rewind"</strong> to prevent having to manually reindex when reconnecting to the correct chain.</li>
<li><strong>Insight Explorer logging fix.</strong></li>
<li><strong>Pre-Blossom EOS halt aligned with 2.0.7</strong> to correct for a mistake in 2.0.7-1 (removed).</li>
</ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->