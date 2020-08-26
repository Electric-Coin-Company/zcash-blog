---
ID: 5066
post_title: 2018 Security Audit Results Overview
post_name: 2018-security-audit-results-overview
post_date: 2019-01-31 12:01:03
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/2018-security-audit-results-overview/
published: true
tags:
  - audit
  - peer review
  - security
  - security audits
categories:
  - General
  - Technical
---
As we embark on a new year with <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/final-blossom-goals/">new goals</a>, the Zcash Company remains committed to the security and safety of our user community. Last year, we published our <a href="/blog/2018-zcash-security-audit-details/">schedule for security audits in 2018</a>. Today, we are excited to announce the results. While the scope primarily pertained to the <a href="https://z.cash/upgrade/overwinter/">Overwinter</a> and <a href="https://z.cash/upgrade/sapling/">Sapling</a> network upgrades, more general reviews of the protocol and code were also conducted.

The result details and our response to each issue are <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/2018-security-audit-results-in-detail/">now available</a> in a detailed format. Those interested in the technical details can follow along with our analysis and read the changes to our source, protocol specification and documentation.
<h2>Summary</h2>
Auditors found a few places where our implementation and specifications differed. Most of the changes that we made to fix this were to clarify the specification and bring it in line with the implementation, which was correct. For example, we added a color scheme to the protocol specification making it clearer which items referred to Overwinter and Sapling.

Two vendors identified that transaction timeouts in their original form could be used to DoS the network, and we have implemented their suggestions. Another issue that was reported to us was considered safe within our implementation, but nevertheless we adapted our application of RedDSA to make it strong for a wide range of uses and we then used it for batch verification later in the development cycle.

In addition, we’ve incorporated the general suggestions vendors made for extra documentation clarity, we’ve ramped-up retrospectives from audits (after issues have been fixed) and we formalized a <a href="/blog/the-zcash-network-upgrade-pipeline/">network upgrade pipeline</a> to bring more time for external security auditing without losing development pace. This year, we plan to introduce more significant security checking into our continuous integration systems.
<h2>Looking Forward</h2>
As we progress with future developments of Zcash, expect ongoing announcements of new audit rounds. Whether features are within the scope of network upgrade releases or significant developments in regular releases which do not require consensus changes, we are still committed to maintaining an open and secure engineering process with a heavy investment in security.

Any worldwide economic infrastructure such as Zcash requires comprehensive review as a fundamental component to user safety. Further, we suggest you bookmark our <a href="https://z.cash/support/security">security information page</a> which includes contact information to report potential security vulnerabilities and links to <a href="https://z.cash/support/security/announcements">security announcements</a> and <a href="https://z.cash/support/security/privacy-security-recommendations">user recommendations</a> pages.