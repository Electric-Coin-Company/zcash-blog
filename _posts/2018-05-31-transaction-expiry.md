---
ID: 3183
post_title: Transaction Expiry
author: Jay Graber
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/transaction-expiry/
published: true
post_date: 2018-05-31 05:38:09
---
<span style="font-weight: 400;">The </span><a href="https://z.cash/upgrade/overwinter.html"><span style="font-weight: 400;">Overwinter</span></a><span style="font-weight: 400;"> network upgrade will include a new feature called ‘Transaction Expiry.’ This will allow transactions in the mempool to expire after a given number of blocks, effectively timing out transactions that are unlikely to be mined and confirmed. All transactions, shielded and transparent, will now have an expiryHeight field that specifies the last block height in which that transaction can be mined.</span>

<span style="font-weight: 400;">When a user submits a transaction to the network, it will persist in the mempool for 20 blocks (approximately 50 minutes). If it has not been mined after that period, it is no longer valid and will be evicted from all mempools. The value will return to the sender’s wallet. For security, zero confirmation transactions should never be assumed to be final and nor the funds spendable. </span>

<span style="font-weight: 400;">Transaction expiry provides senders certainty about their transactions. Implemented as a consensus rule, this is an alternative to other solutions like replace-by-fee which lets users replace an unconfirmed transaction with one that has a higher fee, or a mempool expiry option which drops transactions from the mempool on a local basis but does not stop their propagation through the network.</span>

<span style="font-weight: 400;">Refer to the transaction expiry </span><a href="https://github.com/zcash/zips/blob/master/zip-0203.rst"><span style="font-weight: 400;">ZIP (Zcash Improvement Proposal)</span></a><span style="font-weight: 400;"> for more information and the </span><a href="https://z.cash/support/ux-checklist.html#transactions"><span style="font-weight: 400;">UX guidelines</span></a><span style="font-weight: 400;"> for advice on integrating transaction expiry into your Zcash service or application. </span>