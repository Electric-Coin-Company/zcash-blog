---
ID: 4868
post_title: Zcash Audit Results
post_name: audit-results
post_date: 2016-10-27 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/audit-results/
published: true
tags:
  - cryptography
  - security
  - security audits
categories:
  - General
---
<p>As a security-focused team, made up of world-class talent, we prioritize the security of Zcash users. True security comes from empowering users directly, and to that end, we will always disclose vulnerabilities we find (as soon as we're certain such disclosure won't harm live users), and describe how we have fixed them or how we intend to fix them.</p>
<p>In keeping with that value, and with our launch imminent, it's important to share the full details of our commissioned audits.</p>
<div id="security-recap" class="section">
<h2>Security Recap</h2>
<p>To give context, in April <a class="reference external" href="/blog/fixing-zcash-vulns/">we highlighted a few vulnerabilities</a> in our code that our team found and fixed. In August, <a class="reference external" href="/blog/auditing-zcash/">we announced our work with two top security auditing teams</a>, and we're presenting those security audit results in this post <a id="id1" class="footnote-reference" href="/blog/audit-results#id2">[1]</a>.</p>
<p>We maintain a <a class="reference external" href="https://z.cash/support/security.html">security page</a> on this site with up-to-date security information about Zcash. We also maintain a <a class="reference external" href="https://github.com/zcash/zcash/blob/master/doc/security-warnings.md">security warnings</a> document for each release.</p>
</div>
<div id="security-audits" class="section">
<h2>Security Audits</h2>
<p>Today we are publishing the final reports of each external security auditor we contracted this summer to review our code. We've triaged the issues found and addressed any we considered severe (e.g. could compromise user privacy, lose funds, break consensus, etc...).</p>
<p>Additionally, we've kept in touch with <cite>Bitcoin Core</cite> developers to ensure any findings relating to our codebase (which is derived from <a class="reference external" href="https://github.com/bitcoin/bitcoin/releases/tag/v0.11.2">Bitcoin Core v0.11.2</a>) does not present any substantial risk to Bitcoin users. We also sent private notifications to developers of <a class="reference external" href="https://www.bitcoinunlimited.info/">Bitcoin Unlimited</a>, <a class="reference external" href="https://bitcoinxt.software/">Bitcoin XT</a>, and <a class="reference external" href="https://bitcoinclassic.com/">Bitcoin Classic</a>. We did not contact developers of any other projects derived from the <cite>Bitcoin Core</cite> codebase.</p>
<p>Each of the auditors have prepared reports of their work and findings. They are all hosted on their respective websites. Here we present links to those reports, our issue tracker searches to track their audit work, and their project summaries:</p>
<div id="ncc-group" class="section">
<h3>NCC Group</h3>
<div class="zecc-paragraph-small-margin docutils container">
<p><strong>Report URL:</strong> <a class="reference external" href="https://www.nccgroup.trust/us/our-research/zcash-cryptography-and-code-review/?research=Public+Reports">https://www.nccgroup.trust/us/our-research/zcash-cryptography-and-code-review/?research=Public+Reports</a></p>
<p><strong>Zcash Issue Tracking:</strong> <a class="reference external" href="https://github.com/zcash/zcash/issues?utf8=%E2%9C%93&amp;q=label%3A%22NCC%20finding%22">NCC findings</a></p>
<p><strong>Their Summary:</strong></p>
<blockquote><p>“NCC Group performed a two-part targeted review of the Zcash cryptocurrency implementation. The first part, performed by the Group's Cryptography Services practice, focused on validating that Zcash's implementation adhered to the Zcash Protocol Specification. An assessment looking for security errors within the cryptographic implementation was also performed. The second part was a C++ source code review for vulnerabilities using static and dynamic analysis and fuzz testing. The review also included a cursory assessment of dependent libraries and recommendations for improving software assurance practices at Zcash.</p>
<p>NCC Group identified an issue that would allow an adversary to tamper with the verification and proving keys used by the Zcash daemon as well as a number of C++ coding errors that could result in stack-based buffer overflows, data races, memory use-after-free issues, memory leaks, and other potentially exploitable runtime error conditions. Additionally, most, if not all, third-party open source library dependencies were identified as being out-of-date. In the end, NCC Group did not find any critical severity issues that would undermine the integrity of the Zcash blockchain or undermine the security of confidential transactions during the time that the review was conducted (from August 8 – September 2, 2016).”</p></blockquote>
</div>
</div>
<div id="coinspect" class="section">
<h3>Coinspect</h3>
<div class="zecc-paragraph-small-margin docutils container">
<p><strong>Report URL:</strong> <a class="reference external" href="https://coinspect.com/doc/CoinspectReportZcash2016.pdf">https://coinspect.com/doc/CoinspectReportZcash2016.pdf</a></p>
<p><strong>Their Announcement:</strong> <a class="reference external" href="https://coinspect.com/zcash-security-audit-results">https://coinspect.com/zcash-security-audit-results</a></p>
<p><strong>Zcash Issue Tracking:</strong> <a class="reference external" href="https://github.com/zcash/zcash/issues?utf8=%E2%9C%93&amp;q=label%3A%22Coinspect%20Finding%22">Coinspect findings</a></p>
<p><strong>Their Summary:</strong></p>
<blockquote><p>“Coinspect reviewed Zcash's innovations over the Bitcoin Core source code, focused on evaluating its resistance against specific threats to cryptocurrencies. Coinspect identified high-risk and moderate-risk issues during the assessment that affected the performance and availability of the Zcash p2p network. The security issues identified did not allow remote code execution nor allowed an attacker to steal funds or compromise the privacy of Zcash users. However we found exploitable 51% and isolation attacks with minimum resources.</p>
<p>It is an honor for Coinspect to contribute with our cryptocurrency security experience to the exceptional team behind this exciting project.”</p></blockquote>
</div>
</div>
</div>
<div id="conclusion" class="section">
<h2>Conclusion</h2>
<p>We are committed to serving our users and community, and one of the best ways we can do that is to provide transparency. Zcash is still in a nascent stage, it is experimental and new; users are encouraged to educate themselves about the risks involved in being a direct part of the Zcash protocol and network.</p>
<p>Please join the Zcash developers and community in <a class="reference external" href="https://inviteme.z.cash/">our Slack</a> and <a class="reference external" href="https://forum.z.cash/">Forum</a> conversations.</p>
<table id="id2" class="docutils footnote" frame="void" rules="none">
<colgroup>
<col class="label">
<col></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="/blog/audit-results#id1">[1]</a></td>
<td>Our blog post also <a class="reference external" href="/blog/auditing-zcash#auditors-and-consultants">described our work with Solar Designer</a> who is analyzing our Equihash Proof-of-Work system. We focus on security audits and mitigations in this post, and we'll post the Equihash analysis in a later post.</td>
</tr>
</tbody>
</table>
</div>
<p>&nbsp;</p>
