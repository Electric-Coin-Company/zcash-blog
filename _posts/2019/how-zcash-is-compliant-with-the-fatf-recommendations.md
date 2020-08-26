---
ID: 8720
post_title: >
  How Zcash is Compliant with the FATF
  Recommendations
post_name: >
  how-zcash-is-compliant-with-the-fatf-recommendations
post_date: 2019-09-24 16:28:49
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/how-zcash-is-compliant-with-the-fatf-recommendations/
published: true
tags:
  - Regulation
categories:
  - General
---
<!-- wp:paragraph -->
<p><em>Earlier this year, FATF finalized its recommendations for how the cryptocurrency sector should be regulated from an AML / CFT perspective. The Electric Coin Company provided feedback during the consultation and our head of regulatory relations, Jack Gavigan, took part in the meeting at which the recommendations were finalised. <a href="https://dev-electriccoinco-wordpress.pantheonsite.io/blog/the-fatf-recommendations/">In a previous blog post</a>, Jack described the FATF Recommendations and how they are likely to impact the cryptocurrency sector. In this post, he describes how Zcash is compliant with the FATF Recommendations.&nbsp;</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Zcash is entirely compatible with all requirements that arise from the FATF Recommendations.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In fact, when taking into account the “Travel Rule” requirement, Zcash is <em>more</em> compliant than most other virtual assets.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Below, we take a detailed look at the specific AML / CFT measures referenced in the FATF Recommendations, and describe both how Zcash is compatible with them, and how virtual asset service providers (VASPs) are able to fulfil their AML / CFT obligations.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Customer Due Diligence (CDD)&nbsp;</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Under the FATF recommendations, VASPs are required to undertake CDD measures when establishing a business relationship. The fact that a VASP supports Zcash or that a customer intends to trade Zcash does not impact the VASP’s ability to carry out CDD checks.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In this respect, Zcash is no different from other virtual currencies such as Bitcoin or Ethereum, and VASPs can apply the same CDD processes.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Transaction Monitoring</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Zcash’s privacy-preserving technology does not prevent a VASP from being able to monitor a customer’s transactions with that VASP (e.g. deposits, withdrawals, trades), and comparing transaction patterns and volumes with the expected behaviour, based on the VASP’s understanding of the nature of the customer or their business (as determined during the CDD checks).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>As a party to its customers’ Zcash transactions (either as a recipient, in the case of deposits, or a sender, in the case of withdrawals), a VASP has visibility of the transaction details. This allows the VASP to detect transaction patterns that do not match that customer’s expected behaviour, and investigate further to determine whether the unexpected behaviour is suspicious.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Zcash requires the use of payment addresses for all transactions. This allows VASPs to issue a unique deposit address to each customer, thus allowing Zcash deposits to be unequivocally attributed to a specific customer. Zcash also requires that customers provide a payment address in order to receive withdrawals, allowing VASPs to conduct sanctions screening, or restrict withdrawals to whitelisted addresses.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In this respect, Zcash is no different from other virtual currencies, and the same tools and procedures for transaction monitoring can be applied to Zcash.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Record-keeping</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In the same way that VASPs can monitor a customer’s Zcash transactions, they can also keep records of those transactions.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For deposits, VASPs can record the customer’s identity, the amount of Zcash that was deposited, the destination address (i.e. the deposit address the VASP created for that customer), the source address (where the customer deposits funds from a <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html#zcash-addresses" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">t-address</a>), and the transaction ID.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For withdrawals, VASPs can record the customer’s identity, the amount of Zcash that was withdrawn, the source address (i.e. the VASPs’s address from which the coins are being sent), destination address (whether it is a t-address or a z-address) and the transaction ID.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It is important to note that the VASP always knows the payment address that a Zcash withdrawal is sent to.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The only difference between Zcash and other virtual currencies in terms of the information available to be recorded by the VASP is that if the customer makes a deposit from a <a href="https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html#zcash-addresses" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">z-address</a>, the VASP will not automatically have visibility of the source address. If it wishes to do so, the VASP can request that the customer provide the source address for the VASP’s records. However, this is not a requirement under the FATF Recommendations.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Suspicious Transaction Reports</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The ability to carry out transaction monitoring ensures that a VASP is able to detect any suspicious activity on the part of its customers. The ability to maintain records of its customers’ transactions ensures that the VASP possesses adequate information to make suspicious transactions reports where appropriate.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Travel Rule</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Zcash was designed to be compliant with the Travel Rule. The required originator and beneficiary information can be attached directly to a shielded transaction using the encrypted memo field. As the name implies, the contents of this field are encrypted when the transaction is added to the blockchain, thus preventing inappropriate or unauthorised disclosure of personal information.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A mock-up of how a Zcash wallet might prompt a user to attach the necessary information to a transaction can be seen below:</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":8721} -->
<figure class="wp-block-image"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/09/1-zecwalletSend.jpg" alt="" class="wp-image-8721"/></figure>
<!-- /wp:image -->

<!-- wp:image {"id":8722} -->
<figure class="wp-block-image"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/09/1.5-zecwalletUpdateaddressbook.jpg" alt="" class="wp-image-8722"/></figure>
<!-- /wp:image -->

<!-- wp:image {"id":8723} -->
<figure class="wp-block-image"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/09/2-zecwalletMemo.jpg" alt="" class="wp-image-8723"/></figure>
<!-- /wp:image -->

<!-- wp:image {"id":8724} -->
<figure class="wp-block-image"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/09/3-zecwalletMemoCompliance.jpg" alt="" class="wp-image-8724"/></figure>
<!-- /wp:image -->

<!-- wp:image {"id":8725} -->
<figure class="wp-block-image"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2019/09/4-zecwalletSummary.jpg" alt="" class="wp-image-8725"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><br></p>
<!-- /wp:paragraph -->