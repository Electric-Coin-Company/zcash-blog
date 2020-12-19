---
ID: 9910
post_title: >
  ECC Wallet threat model and security
  assessment results
post_name: >
  ecc-wallet-threat-model-and-security-assessment-results
post_date: 2020-06-18 22:28:51
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/ecc-wallet-threat-model-and-security-assessment-results/
published: true
tags:
  - security
  - wallets
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>ECC open-sourced our work-in-progress iOS and Android Zcash wallets last week, so it makes sense for the ECC security team to provide some transparency into the work we’ve engaged in to help secure them appropriately. It’s been a continuous iterative process, and we’ve been working directly within the wallet team for months to drive, encourage and support the push for secure development. Prior to the release of the code, we performed an in-house security audit, the results of which we are making available now.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Threat model &amp; known issues&nbsp;</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><a rel="noreferrer noopener" href="https://zcash.readthedocs.io/en/latest/rtd_pages/wallet_threat_model.html" target="_blank">Our threat model for the mobile wallets and the SDKs</a> was a huge help in prioritizing security issues against other user concerns and for communicating and aligning with the development team around security issues. It led to better security prioritization decisions and allowed us to safely save on implementing security or privacy properties that were too complicated or of otherwise little or no benefit to users (particularly when they might lead to overconfidence or a false sense of security).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The light wallet protocol that ECC’s example apps use has several known weaknesses that are documented in the threat model. A couple of them deserve to be highlighted here:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>If the lightwalletd server the wallet connects to is compromised or malicious, it could make the wallet display inaccurate transaction information and mislead the user into thinking they received a payment when they did not.</li><li>The acts of sending and receiving transactions have unique traffic patterns that are observable even though the connection is encrypted. This means that it’s possible for an attacker on the network to learn <em>whether</em> a particular address belongs to a user, learn <em>when</em> users are sending/receiving transactions, and, by correlating that information across multiple users, potentially learn <em>whom</em> users are sending/receiving transactions to/from.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Fixing these problems will require research-backed improvements to the light wallet protocol.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Internal security assessment results</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Our internal security assessment focused on the example app codebases, looking for vulnerabilities that might be reachable by a malicious lightwalletd server through the light wallet protocol, by other users through the memo field, or by other apps installed on the same device. The assessment found a few moderate-severity vulnerabilities that were fixed right away, but no high-severity issues that could lead to theft of funds.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>There was a bug in the Android wallet where the Zcash memo field could be used to control official-looking UI text saying where the transaction came from, which could potentially be used for social engineering attacks. The Android wallet also wasn’t checking the checksum in the BIP39 seed phrases, so it was possible for the user to make an error while restoring a seed, and the wallet wouldn’t detect the problem. All of these issues have been fixed in the current codebases.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>On the iOS side, there was a bug caused by the use of null-terminated strings in the communication between the Swift code and librustzcash, so a Zcash address with a null byte followed by more data would pass validation. All of these issues have been fixed too.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Of the remaining issues, the ones we found most interesting are:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>There are a few issues related to the display of the “sent from” address extracted from memo fields. The user interface states (as though it were fact) that the transaction came from the address in the memo, but that isn’t cryptographically guaranteed, so users might be confused. This is something we will feed back into our UI design process to make sure users understand the accuracy of the data they’re looking at.</li><li>The wallets don’t force the user to back up their seed phrase, which we felt could lead to accidental loss of funds. This is left open for the time being because we want to build a better alternative to that forced-backup process, and we're exploring options like only forcing a backup once the wallet has a certain amount of funds or only before an address is displayed, and so on.</li><li>The wallets estimate balance by assuming it only takes one miners’ fee to spend all of the balance, which could be false if an attacker deliberately split their payment up into many parts that would require many blocks worth of transactions to spend. This is an issue in the Zcash protocol and zcashd, see <a href="https://github.com/zcash/zcash/issues/4538" target="_blank" rel="noreferrer noopener">Issue #4538</a> for more details.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>There are some more issues we don’t have the space to discuss here; we would love it if you <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/audit-report-v1.3.pdf" target="_blank" rel="noreferrer noopener">read the full assessment report</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Our approach to threat modeling and testing</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>If you’ve seen threat models before, you’ll find that our <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/wallet_threat_model.html" target="_blank" rel="noreferrer noopener">approach</a> looks a bit different.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Instead of focusing on <em>threat actors</em> (the attackers) like a typical threat model would, this one treats the security properties that users want and care about as the fundamental objects of discussion.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It starts out as an empty list, meaning “there are not yet any intended security properties,” and security properties are only added to the list once there’s some confidence that they’re really true.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In this approach, there are <em>two</em> different ways a security vulnerability can exist:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>If the threat model lists a security property that isn’t actually true, then that’s a security vulnerability in the code, and either the code needs to be fixed or the statement of the property in the threat model needs to be weakened.</li><li>If users are relying on security properties that <em>aren’t</em> listed in the threat model, then that’s just as bad as if there were a security vulnerability in the code. This is a “secure usability vulnerability.” The problem is in the UX and communication with the users. There isn’t necessarily anything wrong with the code, but implementing the missing security property is a valid way to solve the problem.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>We think that the result is a clear and simple threat model that is simpler to maintain and helps the team converge on a shared understanding of the software’s security properties faster.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The threat model was the driving force behind the decision to invest significantly in the <a rel="noreferrer noopener" href="https://github.com/zcash/lightwalletd/blob/master/docs/darksidewalletd.md" target="_blank">“darksidewalletd”</a> testing framework that was started by the security team and then adopted and built upon by the wallet team. It is a testing framework capable of recreating any on-chain activity without the need for generating the actual chain, from the perspective of the lightwalletd server. We use it to more comprehensively test for the wallets’ correct handling of rare block chain reorganizations.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In the future we plan to use it to write tests that harden the wallets against some of the attacks that can be carried out by a compromised or malicious lightwalletd server, that are described in the threat model.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>We batch internal security analysis</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Most of the security input we provide to the wallet team is done in real-time, directly and within their own workflows to provide maximum integration and effect. However, even with that proximity to developer workflow, given how high velocity the wallet team is, it’s not always possible to provide real-time security assessment, and so it often happens in batches. We thought it would be a good idea for user confidence, and to further ECC’s mission to provide general transparency, to provide some insight into that work by publishing a report on security findings resulting from analyzing the security of the mobile wallet example applications.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>We welcome feedback from the community</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Now that the apps are open-sourced, it is possible for anyone to take a look at the applications, our threat model, our analysis and results.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If you’d like to provide feedback, we’re available. If you’ve found a specific bug and you would like to report it, please email <a href="mailto:security@z.cash" target="_blank" rel="noreferrer noopener">security@z.cash</a>, <a href="https://z.cash/gpg-pubkeys/security.asc" target="_blank" rel="noreferrer noopener">ideally encrypted with our PGP key</a>. Any other comments or feedback on our approach to threat modeling of the models themselves, please email me directly at <a href="mailto:taylor@electriccoin.co" target="_blank" rel="noreferrer noopener">taylor@electriccoin.co</a>.</p>
<!-- /wp:paragraph -->