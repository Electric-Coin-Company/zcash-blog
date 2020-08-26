---
ID: 9905
post_title: >
  Heartwood security assessment turns up
  no major issues
post_name: >
  heartwood-security-assessment-turns-up-no-major-issues
post_date: 2020-06-17 21:19:01
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/heartwood-security-assessment-turns-up-no-major-issues/
published: true
tags:
  - security
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>There’s always a lot going on with the ECC security team, and the last few months have been no exception.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A recent Heartwood security assessment conducted by independent firm <a rel="noreferrer noopener" href="https://www.trailofbits.com/" target="_blank">Trail of Bits</a>, revealed no major issues in the implementation of NU3 ZIPs. The final report was handed over May 6, and we are making it <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2020/06/Trail-of-Bits-ZCash-NU3-Implementation-Security-Assessment-final.pdf" target="_blank" rel="noreferrer noopener">publicly available now</a>. It is also available <a rel="noreferrer noopener" href="https://github.com/trailofbits/publications/blob/master/reviews/Zcash2.pdf" target="_blank">from Trail of Bits' Github</a>. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The ECC team was impressed with ToB's depth of knowledge, and they were even able to perform some additional general application-security-assurance activities as a value-add, which was greatly appreciated by our ECC team.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Thanks, Trail of Bits, for another successful engagement.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Results and response</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We received some advice on fuzzing and we're running with it. Other work that coincided with the engagement revealed that a different approach was needed, further validating the move to libfuzzer and away from AFL. We learned it was possible to reuse a substantial part of the effort that had already been put in, but I'm planning on writing a more in-depth review of our fuzzing efforts in an upcoming blog post, so I’ll save the details for then.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Taylor Hornby and Daira Hopwood did some further analysis of a test_bitcoin ASAN issue and discovered that the use-after-free was a problem in the scheduler code itself. But it could only manifest if the scheduler service queue for the same scheduler object was entered in two separate threads — a condition that never occurs in any bitcoin-derived coin that we could think of, including zcashd. We are tracking the improvement as <a href="https://github.com/zcash/zcash/issues/4569" target="_blank" rel="noreferrer noopener">ticket #4569</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Should we continue with these assessments?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>After this latest assessment, we discussed whether we should continue to fund external security assessments for all ZIPs, regardless of their complexity or maximum risk to the network. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We are very lucky to have some of the top experts in cryptography working here, but after considering the implications of any system where we attempt to categorize which ZIPs should and should not receive external security analysis, and in recognition of the need to expand the Zcash ecosystem in a way that provides assurance to users, it was decided that we would continue our policy of external security assessment of each ZIP. In fact, we plan to expand the scope of security assessments to include at least soft fork consensus changes that have been made between network upgrades.</p>
<!-- /wp:paragraph -->