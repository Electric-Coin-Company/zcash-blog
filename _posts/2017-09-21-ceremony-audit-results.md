---
ID: 1550
post_title: Ceremony Audit Results
author: Paige Peterson
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/ceremony-audit-results/
published: true
post_date: 2017-09-21 00:00:00
---
As a science-focused team, ensuring the security of the Zcash protocol and the users of the network is a natural part of our development process. We are committed to serving our users and community, and one of the best ways we can do that is to provide transparency. We've shared the results of <a class="reference external" href="/audit-results/">previous security audits</a> that we contracted <a class="reference external" href="/auditing-zcash/">expert teams to undertake</a>, and we intend to continue doing so on a regular basis.

Today, we're sharing the results of an audit reviewing the <a class="reference external" href="https://z.cash/technology/paramgen.html">parameter generation ceremony</a> which took place just before the launch of the network last year. We contracted with <a class="reference external" href="https://www.nccgroup.trust">NCC Group</a> to analyse artifacts gathered from the station they operated as part of the ceremony. As participants, they had access to the compute node used to generate their shard of the <cite>toxic waste</cite> private key and the commitment hashes created and transferred between the network and compute nodes.

In addition to the production compute node, NCC Group set up a test compute node which was a copy of the production node but modified with forensics capabilities to detect vulnerabilities in the process. This investigation was a protected secret until after the Ceremony completed, as described below in <a class="reference internal" href="#operational-security">Operational Security</a>.

The NCC Group investigation did not reveal any fatal vulnerabilities in the Ceremony. It is important to emphasize that audits and forensics investigation cannot prove the absence of compromise. However, these results are one more of a set of measures the Zcash team undertook to provide strong assurances against compromise.

Remember that the first line of defense was the Multi-Party Computation: in order for an attack to succeed, the attackers would have had to compromise <em>all</em> of the participants in the Ceremony.
<div id="audit-results" class="section">
<h2>Audit Results</h2>
<div class="zecc-paragraph-small-margin docutils container">

<strong>Summary:</strong>
<blockquote>"To perform such attacks, NCC Group and Zcash architected an attack test bed that modeled the ceremony, and NCC Group would operate under the name 'Moses Spears.' NCC Group would (and did) remain in audio/visual contact with the other ceremony members throughout the ceremony. NCC Group performed the tests by setting up a third node that was a copy of the compute node being used in the ceremony. This system was air gapped and used an exact copy of the DVD-R that was used in ceremony.

Each attack was performed by NCC Group and only the DMA attack was successful at extracting memory from the 'test' compute node. The DMA attack was only able to perform a partial extraction of memory. Based on this finding, it is our recommendation that the computation process perform a pre-compute validation step that audits any detected DMA surface areas, namely FireWire, for being present on the device.

After the ceremony was completed, an audit was performed on all of the ceremony media used to boot the live environment. Throughout the audit, no malicious processes were identified and no network listeners, or network transmissions, were attempted by the compute node on boot. Video of the ceremony, when in action, was taken. The facility's closed-circuit video, alarms, and access control systems were operable throughout the ceremony and no anomalous activity was detected during the ceremony.

Based upon the evidence examined by NCC Group, it is our expert opinion that the NCC Group compute node was not compromised throughout the duration of the event."</blockquote>
</div>
You can also read the <a class="reference external" href="https://www.nccgroup.trust/us/our-research/zcash-ceremony-and-audit/?research=Public+Reports">complete NCC Group report</a>.

</div>
<div id="operational-security" class="section">
<h2>Operational Security</h2>
The Zcash team made a best effort at operational security for this investigation. By limiting knowledge of this operation, we strove to maximize the chance of catching any attacker "red-handed".

By intention, within the Zcash team, only Nathan and Zooko knew about this plan until after the Ceremony completed. Communication with NCC Group about this occurred over PGP encrypted emails and some Google Hangout conferences and phone calls. We requested that knowledge of this investigation remain limited within NCC Group, and their team has experience with such internal compartmentalization.

Because the Zcash Company was already engaged with NCC Group for security audits of the Zcash codebase (see <a class="reference external" href="/audit-results/">Audit Results</a>), this provided useful cover for discovery of the operation. For example, we already had regular PGP-encrypted correspondence with NCC Group, and administrative issues like contracts and invoicing could be handled without revealing this operation to a wider audience. An attacker monitoring communication metadata such as would not see noticeable change in who we communicated with.

Notably, Ceremony participants, designers, and engineers were unaware of this operation until after the Ceremony completed. NCC Group used a pseudonymous email address and identity for coordinating their participation in the Ceremony.

Of course, none of this is a guarantee against a compromise, and our operational security wasn't perfect (for example we have no specific knowledge of Google Hangout content confidentiality). It was our best effort given our resources and expertise.

</div>
<div id="conclusion" class="section">
<h2>Conclusion</h2>
Given that a single uncompromised participant in the ceremony suffices for security of the resulting parameters, NCC Group's findings reinforce our confidence in the integrity of the parameter generation ceremony. We will continue to commission independent audits and publish the results as we develop and improve Zcash, especially with the <a class="reference external" href="/tag/sapling/">Sapling cryptography improvements and protocol upgrade</a>. Keep an eye out on our blog for more information on future reports.

</div>