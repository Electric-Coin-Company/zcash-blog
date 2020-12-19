---
ID: 8687
post_title: The FATF Recommendations
post_name: the-fatf-recommendations
post_date: 2019-09-19 14:01:59
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/the-fatf-recommendations/
published: true
tags:
  - Regulation
categories:
  - General
---
<!-- wp:paragraph -->
<p><em>Earlier this year, FATF finalized its recommendations for how the cryptocurrency sector should be regulated from an AML / CFT perspective. The Electric Coin Company provided feedback during the consultation and our head of regulatory relations, Jack Gavigan, took part in the meeting at which the recommendations were finalised. In this blog post (part 1 of 2), he describes the FATF Recommendations and how they are likely to impact the cryptocurrency sector. In part 2, he will describe how Zcash is compliant with the FATF Recommendations.&nbsp;</em></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Background</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The <a href="https://www.fatf-gafi.org/" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Financial Action Task Force</a> (FATF) is an inter-governmental body that develops and promotes policies to prevent money laundering, terrorist financing and the financing of proliferation of weapons of mass destruction. It has issued a series of <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="http://www.fatf-gafi.org/publications/fatfrecommendations/documents/fatf-recommendations.html" target="_blank">Recommendations</a> which are recognised as the global anti-money laundering (AML) and counter-terrorist financing (CFT) standard. The majority of countries across the world have enacted legislation and implemented AML / CFT regulation that complies with the FATF Recommendations.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In June 2015, the FATF issued <a href="https://www.fatf-gafi.org/media/fatf/documents/reports/Guidance-RBA-Virtual-Currencies.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">guidance for a risk-based approach to virtual currencies</a> but did not alter its formal Recommendations.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In July 2018, the United States assumed the chairmanship of FATF and made crytocurrencies a priority. In October 2018, FATF updated the <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="http://www.fatf-gafi.org/media/fatf/documents/recommendations/pdfs/FATF%20Recommendations%202012.pdf" target="_blank">FATF Recommendations</a> by adding the following paragraph to the existing Recommendation 15 (which addresses the risks of New Technologies):</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>To manage and mitigate the risks emerging from virtual assets, countries should ensure that virtual asset service providers are regulated for AML/CFT purposes, and licensed or registered and subject to effective systems for monitoring and ensuring compliance with the relevant measures called for in the FATF Recommendations.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Virtual assets and virtual asset service providers are defined as follows:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p><strong>Virtual Asset</strong> -  A virtual asset is a digital representation of value that can be digitally traded, or transferred, and can be used for payment or investment purposes. Virtual assets do not include digital representations of fiat currencies, securities and other financial assets that are already covered elsewhere in the FATF Recommendations.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p><strong>Virtual Asset Service Providers</strong><br> Virtual asset service provider means any natural or legal person who is not covered elsewhere under the Recommendations, and as a business conducts one or more of the following activities or operations for or on behalf of another natural or legal person:<br> i. exchange between virtual assets and fiat currencies;<br> ii. exchange between one or more forms of virtual assets;<br> iii. transfer* of virtual assets;<br> iv. safekeeping and/or administration of virtual assets or instruments enabling control over virtual assets; and<br> v. participation in and provision of financial services related to an issuer’s offer and/or sale of a virtual asset.<br> (* In this context of virtual assets, transfer means to conduct a transaction on behalf of another natural or legal person that moves a virtual asset from one virtual asset address or account to another.)</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>The FATF provided further background to the change in an <a href="http://www.fatf-gafi.org/publications/fatfrecommendations/documents/regulation-virtual-assets.html" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">explanatory note</a>, calling on all jurisdictions to “urgently take legal and practical steps to prevent the misuse of virtual assets”.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In February 2019, FATF published a <a href="https://www.fatf-gafi.org/publications/fatfrecommendations/documents/regulation-virtual-assets-interpretive-note.html" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">draft of the interpretive note to Recommendation 15</a> which clarified which “relevant measures” FATF intended should be applied to virtual asset service providers (VASPs). FATF invited feedback on paragraph 7(b) which, as drafted, would have applied the same requirements that apply to wire transfers (described in FATF Recommendation 16, and often referred to as the “Travel Rule”) to transfers of virtual assets:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:quote {"className":"is-style-large"} -->
<blockquote class="wp-block-quote is-style-large"><p>Countries should ensure that originating VASPs obtain and hold required and accurate originator information and required beneficiary information on virtual asset transfers, submit the above information to beneficiary VASPs and counterparts (if any), and make it available on request to appropriate authorities. It is not necessary for this information to be attached directly to virtual asset transfers. Countries should ensure that beneficiary VASPs obtain and hold required originator information and required and accurate beneficiary information on virtual asset transfers, and make it available on request to appropriate authorities. Other requirements of R.16 (including monitoring of the availability of information, and taking freezing action and prohibiting transactions with designated persons and entities) apply on the same basis as set out in R.16 </p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>The Travel Rule makes a lot of sense in the context of wire transfers, where both the Sender and Recipient are always financial institutions, the identity of the receiving institution is always known to the Sender, and wire transfers take the form of messages between financial institutions (e.g. SWIFT MT103), which makes it trivial to transmit the necessary information by including it in the payment message. However, virtual asset transfers are fundamentally different. With the exception of Zcash (whose encrypted memo field was designed to facilitate compliance with the Travel Rule), cryptocurrencies do not, in general, enable the transfer of the necessary information as part of a transaction, which means that the information would need to be sent separately. However, the decentralized, permissionless nature of cryptocurrencies means that there are no restrictions on creating cryptocurrency payment addresses, and, therefore, no way to reliably determine whether the recipient of a virtual asset transfer is a VASP or not, and, if so, which VASP it is (which would be necessary in order to be able to send the receiving VASP).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Needless to say, many firms in the crypto sector were alarmed at the prospect of being required to comply with an impracticable requirement and feedback was duly provided to FATF. We contributed to <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.gdf.io/wp-content/uploads/2018/01/GDF-Input-to-the-FATF-public-statement-of-22-Feb-2019-FINAL.pdf" target="_blank">GDF’s response</a> which is worth reading for its in-depth analysis of the draft requirement, and the alternative solutions it proposes.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Recent Developments</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In April, FATF held its annual Private Sector Consultative Forum (PSCF) in Vienna, at which the draft Interpretative Note - and paragraph 7(b) in particular - was discussed extensively. The Forum was attended by several dozen organizations and companies from the cryptocurrency sector, primarily exchanges and blockchain analytics and compliance solutions providers, as well as several industry associations. Only three teams who have created virtual assets were represented: Ripple, Tether, and the Electric Coin Company.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I was later told that it was the most exciting and controversial FATF forum to date, with some “lively” debate about whether the requirements set forth in the draft paragraph 7(b) were reasonable and proportionate. FATF had invited several speakers to present, one of whom, Thomas Hardjano from MIT Connection Science, proposed X.509 certificates as a “silver bullet” solution. However, participants from the cryptocurrency sector expressed concerns that the approach described by Hardjono assumed the existence of digital identity infrastructure that doesn’t currently exist, and failed to address a host of questions and issues, ranging from how the solution would work with BIP-39 wallets to where the liability for inaccurate KYC information would lie.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>At one point, it was suggested (by a former US Treasury official now employed by a large investment bank) that the cryptocurrency sector sought to avoid being regulated altogether, an accusation that many in the room found insulting.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To their credit, FATF acknowledged the concerns raised during the PSCF, and undertook to discuss 7(b) further before finalizing the text.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>FATF’s Final Recommendation</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In June 2019, FATF published the finalized version of the Interpretive Note to Recommendation 15, which can be found on pages 70 and 71 of the <a href="http://www.fatf-gafi.org/media/fatf/documents/recommendations/pdfs/FATF%20Recommendations%202012.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">FATF Recommendations</a>. It essentially requires that countries apply AML / CFT requirements to virtual asset service providers (VASPs) in much the same way that they are applied to financial institutions, and specifies that Recommendations 10 to 21 should be applied to VASPs:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 10 - Requiring that VASPs undertake customer due diligence measures (CDD; often referred to as KYC) when establishing a business relationship with a customer (or where occasional transactions exceed USD/EUR 1,000), and conduct ongoing due diligence on both the business relationship and the customer’s transactions.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 11 - Mandating that VASPs keep records relating to CDD and customer transactions for at least 5 years</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 12 - Special requirements for customers who are politically exposed persons (PEPs)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 13 - Requirements relating to correspondent banking relationships (which is of questionable relevance for VASPs)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 14 - Mandating that countries regulate VASPs by requiring that they are licensed or registered, and subject to AML / CFT requirements</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 15 - Requiring that the AML / CFT risks associated with new financial products, business practises and technologies be identified and assessed</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 16 - Mandating that wire transfers include originator and beneficiary information (the revised paragraph 7(b) - see below - extends this requirements to transfers of virtual assets between VASPs or between a VASP and a financial institution), and that UN Security Council sanctions are enforced&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 17 - Setting standards regarding the use of third parties for CDD</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 18 - Requiring that VASPs implement AML / CFT programmes</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 19 - Requiring that enhanced CDD measures are applies to customers from countries that have been identified by FATF as higher-risk</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 20 - Requires that VASPs report suspicious transactions to the financial intelligence unit</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>R. 21 - Prohibits VASPs from disclosing that a suspicious transaction report has been made</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Paragraph 7(b) was revised to make it clear that the Travel Rule requirement would only apply to transfers of virtual assets between VASPs:</p>
<!-- /wp:paragraph -->

<!-- wp:quote {"className":"is-style-large"} -->
<blockquote class="wp-block-quote is-style-large"><p>Countries should ensure that originating VASPs obtain and hold required and accurate originator information and required beneficiary information on virtual asset transfers, submit the above information to the beneficiary VASP or financial institution (if any) immediately and securely, and make it available on request to appropriate authorities. Countries should ensure that beneficiary VASPs obtain and hold required originator information and required and accurate beneficiary information on virtual asset transfers and make it available on request to appropriate authorities. Other requirements of R. 16 (including monitoring of the availability of information, and taking freezing action and prohibiting transactions with designated persons and entities) apply on the same basis as set out in R. 16. The same obligations apply to financial institutions when sending or receiving virtual asset transfers on behalf of a customer.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:heading -->
<h2>Implications for the Cryptocurrency Sector</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Most of the requirements came as no surprise and (as might be expected, given that the Recommendation was adopted during the United States’ chairmanship of FATF) are very similar to the regulatory regime that cryptocurrency exchanges are subject to in the United States (and will be subject to in the European Union, when the Fifth AML Directive is implemented in early 2020).&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>As other countries adopt legislation that implements the FATF Recommendations, a similar baseline set of requirements will be imposed across jurisdictions, and opportunities for “regulatory arbitrage” will diminish. Major exchanges in the US and EU, such as Bitstamp, Coinbase, Gemini and Poloniex, are already compliant with the majority of the FATF requirements, so exchanges in other jurisdictions should have no problem complying with the same requirements. That said, it’s important to note that FATF’s Recommendations are directed at governments, who then follow the Recommendations when drafting relevant legislation or regulations. As such, different countries implement the Recommendations in different ways, and some countries may impose requirements that are more stringent than the FATF Recommendations.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The FATF Recommendation includes two new requirements that have not previously been imposed: a USD/EUR 1,000 threshold for occasional transactions, and the 7(b) Travel Rule.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The USD/EUR 1,000 threshold applies when the VASP engages in occasional transactions with a customer, and does not have an ongoing business relationship with them (and, therefore, is not required to conduct CDD when establishing a business relationship). This requirement seems likely to have the most impact the cryptocurrency ATM business model, where providers will likely be required to start identifying all customers in order to detect when the cumulative value of multiple transactions crosses the threshold.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The 7(b) Travel Rule is the most significant requirement. In principle, it requires that VASPs require their customers provide information about the originator or beneficiary of any virtual asset transfer the VASP receives (e.g. a deposit into the customer’s account with the VASP) or carries out (e.g. a withdrawal from the customer’s account) on behalf of that customer, including whether the originator or beneficiary’s address is custodied at another VASP and, if so, which VASP.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If the originator or beneficiary’s address is not custodied at another VASP, no further action is required (other than storing the information for at least five years), and the VASP can process the transfer as normal.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If, on the other hand, the originator or beneficiary’s address <em>is</em> custodied at another VASP, the VASP must take some action.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The originating VASP must send “required and accurate originator information and required beneficiary information” to the beneficiary VASP. The wording here is important. While the originator information must be “accurate” (which is trivial to ensure, as the originating VASP will already have KYC’d the originator), the originating VASP is not obligated to verify that the beneficiary information is accurate. In other words, they are permitted to accept, at face value, the information provided by the customer.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Similarly, the beneficiary VASP is required to “obtain and hold required originator information and required and accurate beneficiary information”, meaning that there is no requirement to verify the accuracy of the information provided to them by their customer (or the originating VASP) in relation to transfers into the customer’s account.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Beneficiary VASPs are also required to verify that the beneficiary information supplied in relation to a transfer from another VASP is accurate (i.e. matches the name of the account that the beneficiary payment address is associated with), and to take appropriate action. Similarly, beneficiary VASPs are likely to be required to take appropriate action if they receive a transfer from another VASP that is not accompanied like the required information.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The required originator and beneficiary information is specified to be the same as that required for wire transfers:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>the name of the originator;&nbsp;</li><li>the originator account number where such an account is used to process the transaction;&nbsp;</li><li>the originator’s address, or national identity number, or customer identification number, or date and place of birth;&nbsp;</li><li>the name of the beneficiary; and&nbsp;</li><li>the beneficiary account number where such an account is used to process the transaction.&nbsp;</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>A footnote to paragraph 7(b) specifies that “the equivalent information in a virtual asset context” may be used instead. For example, it seems likely that payment addresses could substitute for account numbers.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>FATF defines a “customer identification number” as “a number which uniquely identifies the originator to the originating financial institution” and “must refer to a record held by the originating financial institution which contains at least one of the following: the customer address, a national identity number, or a date and place of birth.”</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Assuming the use of a customer identification number, an example of the required information might look something like this:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<blockquote class="wp-block-quote is-style-large"><pre>Originating VASP: Gemini
Originator Name: Satoshi Nakamoto
Originator Payment Address: 12cbQLTFMXRnSzktFkuoG3eHoMeFtpTu3S
Originator Customer Identification Number: GEM-SN001
Beneficiary VASP: Coinbase 
Beneficiary Name: Hal Finney <br>Beneficiary Payment Address: 1Q2TWHE3GMdB6BZKafqwxXtWAWgFt5Jvm3</pre></blockquote>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>With wire transfers, the beneficiary and originator information must be attached directly to the wire transfer message (i.e. the information must “travel” along with the wire transfer). The Zcash protocol was designed with this requirement in mind, and the required information can be attached to a shielded transaction using the encrypted memo field.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>However, most other virtual assets have no mechanism for attaching this type of information to a transaction, so FATF has specified that it is “not necessary for this information to be attached directly to the virtual asset transfers”. In theory, it could be sent via email or submitted using a web form on the beneficiary VASP’s website.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A number of initiatives are investigating potential industry-wide solutions or standards to address this requirement for virtual assets that do not provide the ability to attach the required information to the transaction.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>However, one option is for VASPs to simply mandate that their customers only deposit virtual assets from, and withdraw virtual assets to, a payment address that the customer herself controls. This would ensure that the VASP neither receives nor sends any virtual asset transfers from or to another VASP, thus avoiding the Travel Rule requirement entirely.&nbsp;</p>
<!-- /wp:paragraph -->