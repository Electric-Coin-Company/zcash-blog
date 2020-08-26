---
ID: 4942
post_title: 'Payment Contexts &#038; Reusing Shielded Addresses'
post_name: shielded-address-contexts
post_date: 2017-04-19 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/shielded-address-contexts/
published: true
tags:
  - explainers
  - privacy
  - transactions
categories:
  - General
---
<p>The privacy provided in Zcash allows users to disclose a shielded payment address publicly or to multiple individuals without the worry of transactions sent to that address <a class="reference external" href="/blog/transaction-linkability">becoming linked in the blockchain</a>. When sending to or from a shielded address, the data involved in that side of the transaction is encrypted (regardless if receiving from or sending to a transparent address).</p>
<div class="figure align-center">
<img alt="Data revealed for a single shielded address" class="center-image" src="/wp-content/uploads/2018/09/simple-z.png"/></div>
<div class="section" id="distinct-payment-contexts">
<h2>Distinct Payment Contexts</h2>
<p>While shielded addresses are encrypted, the scope of the payment address is something to consider.</p>
<p>If Alice has a small business she runs out of her home, any business mail sent to her home address provides a clear link between her personal life and business even if the details of the correspondences are secured in envelopes. In a similar fashion, if Alice has a business which accepts Zcash for services or products and personal blog which she posts the same Zcash address for accepting donations to, it is possible for a third-party to correlate the business and blog.</p>
<p>It is therefore recommended for Alice to use separate payment addresses for her business and blog, similar to having a separate business address (such as a private mailbox) for receiving business correspondence.</p>
</div>
<div class="section" id="reusing-shielded-addresses">
<h2>Reusing Shielded Addresses</h2>
<p>Note that it <em>is</em> advisable to reuse shielded addresses for receiving payments within the same context. While it has become standard practice for generating a new address for each receiving transaction in most cryptocurrencies, that is not a problem when using shielded addresses. In fact, it saves the extra hassle of tracking many different addresses <em>and</em> reduces the number of outputs consumed when creating a new transaction. This reduction makes overall transaction size smaller and requires less resources for generating a zero-knowledge proof.</p>
<p>A great example of this distinction can be seen on the <a class="reference external" href="https://riseup.net/donate">donations page</a> for the non-profit Riseup.net. When a supporter goes to make a bitcoin donation, they're provided with a newly generated address but when a supporter makes a Zcash donation, the same shielded address is provided for everyone!</p>
</div>
<div class="section" id="one-shielded-address-per-purpose">
<h2>One Shielded Address Per Purpose</h2>
<p>We encourage folks to follow suit and reuse shielded addresses for accepting Zcash payments within the same context. For contexts which should remain unassociated, however, make sure to keep the shielded addresses unassociated as well.</p>
<p>For more user privacy considerations, see the <a class="reference external" href="https://z.cash/support/security/privacy-security-recommendations.html">Privacy &amp; Security Recommendations</a>.</p>
</div>
