---
ID: 4896
post_title: >
  The Metamorphosis of Malleable
  Transactions
post_name: metamorphosis-of-malleable-transactions
post_date: 2016-08-31 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/metamorphosis-of-malleable-transactions/
published: true
tags:
  - bitcoin
  - software
  - transaction malleability
categories:
  - General
---
<p>Transaction malleability has been a long-standing issue for Bitcoin-derived cryptocurrencies and it's an issue which the Zcash team have been keen to address. Let's explore what the problem is and why it's important to solve in the long run.</p>
<p>In a nutshell, transaction malleability is where a valid transaction can be modified in-flight as it propagates across the network. The details can be found <a class="reference external" href="https://github.com/bitcoin/bips/blob/master/bip-0062.mediawiki">here</a>.  While the modifier doesn't have access to the private keys of the sender and is unable to steal funds for personal gain, the modified transaction does pose a problem because it can be considered valid by the network. That is, there could be two transactions attempting to spend the same coins but with different transaction IDs.</p>
<p>Although such modifications are often thought to be just a <a class="reference external" href="https://cointelegraph.com/news/the-ongoing-bitcoin-malleability-attack">nuisance</a>, transaction malleability does have real-world impact. First, wallet software cannot rely on a transaction ID to track a movement of funds.  Second, businesses relying on chained transactions, where the change from one transaction is spent immediately in a new transaction, will find that the chain can be broken.  Thirdly, off-chain solutions designed to improve transaction throughput, such as <a class="reference external" href="https://lightning.network/">Lightning</a> and <a class="reference external" href="/blog/bolt-private-payment-channels/">BOLT</a>, are more practical if transaction malleability is first solved.</p>
<p>So how to fix malleability?  One solution proposed to us has been to back-port <a class="reference external" href="https://bitcoincore.org/en/2016/01/26/segwit-benefits/">Segregated Witness</a> (segwit) which addresses a range of issues including malleability.  However, <a class="reference external" href="https://github.com/zcash/zcash/issues/451">it was decided</a> a few months ago that it was not possible to do so within the Zcash project’s timeline, especially as segwit was a work-in-progress at the time.  Today, development of segwit is <a class="reference external" href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2016-September/013098.html">mostly complete</a>, but it has yet to be deployed and activated across the Bitcoin network.</p>
<p>Our own attempt at a smaller and more focused solution was released a few weeks ago as part of the <a class="reference external" href="/blog/new-alpha-release-optimization-and-nonmalleability/">z8 alpha release</a> and deployed to the test network.  Although no issues cropped up in daily use, we had always been conscious that there might be edge cases and security concerns we had not yet detected.  In fact, there is a bug where a newly mined block could be modified posing a risk of denial-of-service, which fortunately was found by our auditors as part of the <a class="reference external" href="/blog/auditing-zcash/">security audit</a> of Zcash. Although the fix itself is fairly simple, the ensuing <a class="reference external" href="https://github.com/zcash/zcash/issues/1304">discussion</a> raised a number of issues for the team to evaluate in order to provide a comprehensive and robust solution.</p>
<p>After consideration, given the available resources and the project schedule, the team have decided to roll back the changes made. We feel it would be prudent to launch with known knowns rather than introduce new unknowns. Our exploration of transaction malleability highlights the importance of independent third-party review to the development process, especially around the consensus protocol where even the smallest of changes can ripple out with hard-to-predict Kafkaesque side effects. We are grateful to our auditors <a class="reference external" href="http://coinspect.com/">Coinspect</a> for helping us to catch some butterflies!</p>
<p>Please help us by running the latest <a class="reference external" href="/blog/new-alpha-release-solidifying-the-consensus-protocol/">z9 alpha release</a> of Zcash and letting us know of any bugs, issues and usability problems you come across.  You can reach the team by filing a <a class="reference external" href="https://github.com/zcash/zcash/issues">GitHub issue</a> or visiting the <a class="reference external" href="https://zcashcommunity.slack.com/messages/zcash/">Zcash Community Slack</a> channel.  Thank you.</p>
