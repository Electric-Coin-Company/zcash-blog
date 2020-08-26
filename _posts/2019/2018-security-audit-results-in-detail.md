---
ID: 6267
post_title: 2018 Security Audit Results in Detail
post_name: 2018-security-audit-results-in-detail
post_date: 2019-01-31 12:00:24
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/2018-security-audit-results-in-detail/
published: true
tags:
  - audit
  - peer review
  - security
  - security audits
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>Today we are announcing the security audit results from five expert security auditors who <a href="/blog/2018-zcash-security-audit-details/">we contracted last year</a>. We hired these experts to conduct comprehensive security and design audits in support of the <a href="https://z.cash/upgrade/overwinter">Overwinter</a> and <a href="https://z.cash/upgrade/sapling">Sapling</a> releases. The summary and implication of the results are available <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/2018-security-audit-results-overview/">here</a> in addition to the result details, our reasoning and response below.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Least Authority, Part 1</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Least Authority have <a href="https://leastauthority.com/blog/releasing-three-zcash-security-audit-reports/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">published their work</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue A: pow leaks in windowed_exp</h5>
<!-- /wp:heading -->

<!-- wp:heading {"level":5} -->
<h5>... and ...</h5>
<!-- /wp:heading -->

<!-- wp:heading {"level":5} -->
<h5>Issue B: Exponent leaks via power function</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>These issues correctly identify cache-snooping attacks that are exploitable by an attacker who is able to run code on the same core. Zcash is not intended to be safe to side-channel attacks in these scenarios, and this is listed <a href="https://github.com/zcash/zcash/blob/master/doc/security-warnings.md" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">in the security warnings in our repository</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue C: Undefined behavior in ​crypto/common.h</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We raised issue <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/1249" target="_blank">#1249</a> which was then later closed by <a href="https://github.com/zcash/zcash/pull/3181" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3181</a>, which includes a commit that clarifies the pointer size and number of points in a way that works on all platforms.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue D: Undefined behavior in CBaseDataStream::read</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We raised issue <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3182" target="_blank">#3182</a> which was then later closed by <a href="https://github.com/zcash/zcash/pull/3183" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3183</a> which added explicit checks for a NULL pointer value before the value gets used.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue E: CTxMemPool::check() does nothing when turned on</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We raised issue <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3134" target="_blank">#3134</a> which was then later closed by <a href="https://github.com/zcash/zcash/pull/3160" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3160</a> which adds an explicit cast as recommended in the issue, and also adds a test to <code>mempool_tests.cpp</code> to check for regressions in this issue.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue F: Transaction expiry reduces safety in reorgs</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Since this issue was not listed as a vulnerability, no changes were made in response to this issue.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Coinspect</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Coinspect have published their <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://coinspect.com/doc/CoinspectReportZcash2018.pdf" target="_blank">assessment of Overwinter</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The numbering of these issues is a continuation of the work that Coinspect did on Zcash in 2016.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>ZEC-012: Transaction Expiry Enables Node Isolation Attack High </h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This attack describes the sequence of events that could use a combination of transaction expiry and network banning to isolate any node from the network.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>ZEC-013: Transaction Expiry Enables Transaction Flooding at No Cost</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We made modifications to our code to fix both these issues in <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/pull/3144" target="_blank">PR 3144</a>.<br>Placeholder issues <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3141" target="_blank">#3141</a> and <a href="https://github.com/zcash/zcash/issues/3142" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3142</a> were used prior to the above implementation.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>NCC Group</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>NCC have <a href="https://www.nccgroup.trust/us/our-research/zcash-overwinter-consensus-and-sapling-cryptography-review/?research=Public+Reports">published their work</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Overwinter Issues</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-001: Asynchronous Chain Updates Can Lead To Network Bans</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This issue is similar to those discovered by Coinspect and remediated there (see Coinspect audit results post). The report includes a retest of this issue, referring to the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/commit/473a1132419d05911933ac0095b207c4e2fc59f3" target="_blank">fix commit</a>&nbsp;which was included in <a href="https://github.com/zcash/zcash/pull/3148" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 3148</a>&nbsp;and fixes both the Coinspect reported issues and this one to a level we are satisfied with.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-002: Mempool Not Properly Cleared if Connecting or Disconnecting Tips Fails</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We decided to temporarily accept this small risk, and it ended up not causing a problem during activation of Overwinter or Sapling. We have raised issue <a href="https://github.com/zcash/zcash/issues/3797" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3797</a> to track for future network upgrades.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sapling Issues</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>These are ordered to match the report to make the task of correlating the findings in the report with our responses simpler.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-004: Curve BLS12-381 Security Is Less Than 128 Bits</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As the issue rightly points out, the existing analysis of this curve puts a practical attack well beyond the foreseeable computing power available to humanity, although we will monitor the research situation as time progresses. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The research mentioned in the issue was also referenced in our <a href="/blog/new-snark-curve/">blog post on curve selection</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We are satisfied that use of this curve strikes an appropriate balance between security and performance.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-009: RedDSA / RedJubjub Are Not Strongly Unforgeable With Re-Randomized Keys</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This issue correctly identified an error in the construction of the RedDSA signature scheme relative to its claimed security properties. There are two relevant ways of formalizing unforgeability for signature schemes: “existential unforgeability” (sufficient for most uses) and “strong unforgeability” (also preventing some forms of malleability). The latter property was claimed but not met <em>in general</em> by the specified scheme, even though it was met (for a designed reason, not by accident) for its uses in Zcash. This error has been corrected in version <em>2018.0-beta-20</em> and later of the <a href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">protocol specification</a>, so that the scheme is now conjectured (and provisionally proven, subject to further review of the proof) to meet the stronger property in general. The relevant change was to move responsibility for ensuring that the public key is included in the hash function input, from the protocol using RedDSA to the RedDSA scheme itself. This correction did not require any visible consensus rule change for Zcash, but it makes RedDSA more safely reusable in other protocols.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-010: Bit Ordering Convention Leads To Mismatches And Confusion</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We took the point that the bit ordering was confusing and issued <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash-hackworks/sapling-crypto/pull/72" target="_blank">PR #72</a> in sapling-crypto to move the implementation to all little-endian and made changes to reflect this in the specification, which were logged in the changelog under version <em>2018.0-beta-15</em> of the <a href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">protocol specification</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-003: Private Key Decoding Has Limited Interoperability</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We opened issue <a href="https://github.com/zcash/zcash/issues/3155" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3155</a> to discuss this but since the issue is not exploitable, no changes have been made to the code in response.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-007: Discrepancies Between Specification and Circuit Implementation</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We have harmonized the implementation and protocol by altering the definition in section 5.4.7.2 “Windowed Pederson commitments” to reflect the order of operations used in the circuit implementation.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-008: Typographical Inconsistencies in Zcash Specification</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This finding was addressed in four parts:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>We have modified the specification to match the order of the two commutative inputs for those definitions to provide clarity in the specification;</li><li>We have corrected the definition of Pederson hash chunking in the specification to bring it in line with the implementation;</li><li>We have corrected the typo, both words now read “RedDSA.RandomizePublic”;</li><li>We have added the definition used in the implementation.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>The changes recommended in this issue were made in version <em>2018.0-beta-20</em> of the <a href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">protocol specification</a> and are listed in the changelog for that version.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>NCC-2018-011: Bias in Random Field Element Generators for Underlying Representation </h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This issue is listed as not exploitable and no changes have been made in response to this issue.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Least Authority, Part 2</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Least Authority have <a href="https://leastauthority.com/blog/releasing-three-zcash-security-audit-reports/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">published their work</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue A: Spec is inconsistent regarding fOverwintered</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This was indeed a typo, as the issue text suggests, which was fixed in a later version. Additionally, we took their general advice to make consensus rules more clear and provided Sapling- and Overwinter-specific consensus changes in different colors for clarity.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue B: Transparent address encoding is compressed</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This was a legitimate oversight on our part and the text has been updated in-line with the recommendation from Least Authority. Section 5.6.1 now reads “of ​<strong>a​ </strong>​<strong>compressed​ </strong>ECDSA key encoding”.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Kudelski Security</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Kudelski Security have <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://research.kudelskisecurity.com/2019/01/31/audit-of-zcashs-sapling-update/" target="_blank">published a blog post on the work&nbsp;they&nbsp;did&nbsp;for&nbsp;us</a>. Their <a href="https://cybermashup.files.wordpress.com/2018/08/zcash-audit.pdf">official report</a> is available.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>PAIRING-001: Unbounded exponent in exponentiation</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The concern was that without an upper bound on the 64-bit integers passed into this part of the code, performance might be degraded to the point of causing a denial-of-service condition. In fact, the calling code ensures that such large numbers are never passed to this location, and we decided that adding a redundant check would incur an unacceptable performance penalty for no gain. Other users of this library should be sure to use it safely, too.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>PAIRING-002: RNG choice delegated to callers</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We deliberately left the choice of random number generators to the caller to improve testability of the code. In Zcash, we’re happy that the rng we pass to the library is appropriate.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>BELLMAN-001: Outdated and unmaintained dependencies</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>While it’s true that these dependencies are marked as unmaintained, we do not currently believe them to be dangerous. Nevertheless we’ve added them to our list of dependencies to swap out and will do so at a more appropriate time.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>BELLMAN-002: Lossy cast to usize</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The use of this variable is defined as being limited to the scope of available memory, and so its use as a length is at least theoretically-valid; however, code changes were made to prevent an out-of-range value from being lost. Specifically the storage of that value is now 32-bit throughout. In practice this makes no appreciable difference since the elements are each 96 bytes long. Any error handling resulting from indexes that are too large to be stored in the array should be handled by the caller.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>These changes were merged into master of zkcrypto/bellman <a href="https://github.com/zkcrypto/bellman/pull/22/commits/6ec7272586a073e1b37417ff10c2818beda18d39" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 22</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>BELLMAN-003: Potential DoS through user-controlled length argument</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Although the length value might be user-controlled, each time the loop over <code>len</code> executes, it calls a generic reader interface provided by the caller (e.g. through <code>read_g1</code> to R) which should fail in such a way that the loop does not execute again when no more data is available, and so no attempt is made to address memory beyond the available values. It is the responsibility of the caller to prevent the DoS condition within this design pattern, and that is the case in Zcash.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>QED-it</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>QED-it have published <a href="https://medium.com/qed-it/sapling-audit-9b531be9d30">a blog post on the work they did for us</a>. Their official report is <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://qed-it.com/sapling-audit-report.pdf" target="_blank">available from their site</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Issues</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>Incorrect assertion - Pedersen hash generators linear relation validation</strong> </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>... and ...</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>Window base patterns generation not matching the spec</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>These two issues refer to an <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash-hackworks/sapling-crypto/pull/75" target="_blank">unmerged pull request</a> to sapling-crypto. That PR has been closed and superseded by <a href="https://github.com/zcash-hackworks/sapling-crypto/pull/95" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">PR 95</a>, which only changes comments and does not have the mentioned issues.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>jubjub::Fs usage is sometimes confusing regarding the prime subgroup</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Fs is intended to represent scalars in the prime subgroup. It is not possible to make the Jubjub implementation only usable within the prime subgroup because the specification allows points outside the subgroup to appear in transaction fields, for performance reasons. We acknowledge that this requires extreme care; alternatives such as Ristretto were not sufficiently developed/understood at the time most of Sapling was designed, and have disadvantages for circuit efficiency.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We filed issue <a href="https://github.com/zcash-hackworks/sapling-crypto/issues/89" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#89</a> to consider other approaches in future protocol upgrades.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Pedersen hash circuit implementation can not calculate inputs larger than 63*3*4</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This does not affect correctness of the circuit for the input sizes used, but will be fixed. We filed issue <a href="https://github.com/zcash-hackworks/sapling-crypto/issues/90" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#90</a> to track this.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>The bit unpacking between layers of the Merkle tree</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In fact it does not reduce the concrete security of the Merkle tree, even by a fraction of a bit. Observe that in attempting to find a second-preimage authentication path for a given root, an adversary has a free choice of the sibling hashes in the path. The choice of congruency gives the adversary no additional power, since at each node in the path, varying the congruency would produce a different root hash in the same way as varying the sibling hash. This issue <a href="https://github.com/zcash/zcash/issues/2234#issuecomment-342149213" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">was considered in the design</a>. The only property needed of the Pedersen hash <em>MerkleCRH</em><sup><em>Sapling</em></sup>, in order for a different congruency to produce a different root hash, is that it is collision-resistant <sup>[*]</sup> on bit-sequence inputs. This tightly reduces to hardness of the DLP on the prime-order subgroup of Jubjub, assuming that <em>FindGroupHash</em> outputs generators that are randomly distributed on this subgroup.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><sup>[*]</sup> Collision-resistance of the hash function implies collision resistance of the Merkle tree, which in turn implies second-preimage resistance of the Merkle tree. In the general case, there are subtle technical obstacles to proving second-preimage resistance of the tree based only on second-preimage resistance of the hash (the heuristic of proving security for a keyed hash and extrapolating to an unkeyed hash does not work). In this context we have to assume hardness of DLP on the prime-order subgroup of Jubjub in any case for the rest of the Sapling protocol, so there would be no benefit to making a second-preimage assumption about <em>MerkleCRH</em><sup><em>Sapling</em></sup> (in fact, breaking DLP breaks second-preimage resistance as well as collision resistance of this hash, so the two assumptions are equivalent in strength).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Testing is done with another implementation of ConstraintSystem</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Note that both implementations (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash-hackworks/sapling-crypto/blob/827e85547e5aaf6bce2b984ee3a0e76da3034af2/src/circuit/test/mod.rs#L368" target="_blank">here</a> and <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zkcrypto/bellman/blob/96b2d3e41a22de4263ee967ab8a6c776c083a048/src/groth16/prover.rs#L99" target="_blank">here</a>) are very simple and short; they are essentially only keeping track of lists of auxiliary variables, inputs, and R1CS constraints. On the other hand, it does seem as though it might be possible to alleviate this concern for future reviews by sharing more code. This is filed as issue <a href="https://github.com/zcash-hackworks/sapling-crypto/issues/92" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#92</a>.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>params.montgomery_2a doesn't seem to be used anywhere</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Indeed, it only seems to be used in <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/librustzcash/blob/e1c6232dd7a5368aa9342649d73db27522cc8d6e/sapling-crypto/src/jubjub/tests.rs#L311-L317" target="_blank">this test</a>. This issue is filed as issue <a href="https://github.com/zcash-hackworks/sapling-crypto/issues/93" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#93</a>.<br></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3><span>Spec&nbsp;notation&nbsp;mismatches&nbsp;and&nbsp;missing&nbsp;parts</span></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Most of these observations have merit, the most severe of them were fixed right away, and for the remainder we have filed issues: <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/issues/176" target="_blank">#176</a>, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/issues/177" target="_blank">#177</a>, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/issues/180" target="_blank">#180</a>, <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/issues/181" target="_blank">#181</a> and <a href="https://github.com/zcash/zips/issues/182" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#182</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In section A.3.3, Theorem A.3.3 is actually stated for any Montgomery curve, so it is was incorrect to reference <em>A</em>​<sub>𝕄</sub> or <em>B</em>​<sub>𝕄</sub> in the proof; it should have referenced just <em>A</em> and&nbsp;<em>B</em>. This is fixed in version <em>2018.0-beta-31</em>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In respect to Theorem A.3.2, the intended condition was “<em>u</em>&nbsp;=&nbsp;0 or 1&nbsp;−&nbsp;<em>v</em>&nbsp;=&nbsp;0”. That there are also no other points in the subgroup with <em>v</em>&nbsp;=&nbsp;0 is true, but not needed. This is fixed in version <em>2018.0-beta-31</em> (the correction to the proof requires a property of complete twisted Edwards curves that was not previously mentioned, so it wasn’t entirely trivial).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We filed issue <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zips/issues/183" target="_blank">#183</a> for the specification and issue <a href="https://github.com/zcash-hackworks/sapling-crypto/issues/91" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#91</a> for the sapling-crypto implementation.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Least Authority, Part 3</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Least Authority have <a href="https://leastauthority.com/blog/releasing-three-zcash-security-audit-reports/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">published their work</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Issue A: RPC HTTP Server is Vulnerable to DNS-Rebinding Attacks</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We have a password mechanism in place, and even recently selectively incorporated Bitcoin's auth cookies in the case where you haven't set a password. Nevertheless, in response to this finding we have updated our documentation on the use of passwords in the RPC interface, and have raised issue <a href="https://github.com/zcash/zcash/issues/3791" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3791</a> to look at further defense-in-depth measures.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Issue B: Instance of Undefined Behavior </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is a useful finding, and we have raised issue <a href="https://github.com/zcash/zcash/issues/3792" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3792</a> to fix it. Note that it is Low impact and requires RPC authentication to access.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Issue C: Transaction Details Disclosure Vector </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is a useful finding, and we have raised issue <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://github.com/zcash/zcash/issues/3793" target="_blank">#3793</a> to discuss possible changes to improve this situation. Note that users should never run zcashd on the same computer that adversarial users can execute code on, because of <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/security_warnings.html" target="_blank" rel="noreferrer noopener" label=" (opens in a new tab)">known weakness to side-channel attacks</a>. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Issue D: Address Interpretation Surprise </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Bech32 encoding is not accepted for Sapling addresses, however we have opened issue <a href="https://github.com/zcash/zcash/issues/3794" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3794</a> and plan to add tests that confirm this to be the case on a continuous basis.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Issue E: Unclear Transaction Interpretation </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We have opened issue <a href="https://github.com/zcash/zcash/issues/3795" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3795</a> for this issue to remove the ambiguity here so that users don't get surprised.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Suggestion1: Strengthen the wallet password system</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We have opened issue <a href="https://github.com/zcash/zcash/issues/3796" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">#3796</a> to discuss the ways we could improve the wallet encryption experience for users.</p>
<!-- /wp:paragraph -->