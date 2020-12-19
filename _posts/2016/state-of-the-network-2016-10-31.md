---
ID: 4957
post_title: State of the Network
post_name: state-of-the-network-2016-10-31
post_date: 2016-10-31 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/state-of-the-network-2016-10-31/
published: true
tags:
  - bugs
  - "Founders' Reward"
  - launch
  - mining
  - sprout
  - State of the Network
categories:
  - General
---
<p>The launch of Zcash 1.0 “Sprout” worked! The blockchain is live. Mining and transactions are working. This is a brief round-up of news from the network.</p>
<hr class="docutils"/>
<p>I found <a class="reference external" href="https://explorer.zcha.in/">this explorer</a> that shows recent blocks, transactions, and statistics. (I have no idea who runs it, and they, of course, don't require our permission to set up such a service. That's just one example of the <a class="reference external" href="/blog/third-party-support/">permissionless innovation</a> that permeates cryptocurrencies.)</p>
<hr class="docutils"/>
<p>There is one known bug, which causes private transactions (those in which all of the inputs and outputs are shielded addresses) to not get mined. We're going to release v1.0.1 shortly to fix it. In the meantime, if you're running a miner, please add <cite>blockminsize=300000</cite> to your <cite>zcash.conf</cite> and restart your miner. You can track the progress on this at <a class="reference external" href="https://github.com/zcash/zcash/issues/1705">issue #1705</a>.</p>
<hr class="docutils"/>
<p>There was a brief DDoS attack yesterday. Our web site (<a class="reference external" href="https://z.cash">https://z.cash</a>) was down for a bit while we engaged DDoS defenses. You should be aware of <a class="reference external" href="https://z.cash/support/security.html">our security page</a> on which we'll log such events.</p>
<hr class="docutils"/>
<p>The supply of ZEC units began at zero on October 28, and it is currently around 1900 ZEC. Currently every block (which arrives, on average, every two and a half minutes) adds about 1.2 ZEC to the supply. However, the amount of newly-generated ZEC which comes in every block is increasing. Therefore, not only is the supply growing, but it is growing faster and faster over time. Here's a graph of the rate at which the supply is increasing during the first couple of months:</p>
<div class="figure align-center" style="width: 75%">
<img alt="ZEC distribution rate for first 30,000 blocks" src="/wp-content/uploads/2016/11/slow-start-rate-30k.png"/></p>
<p class="caption">ZEC distribution rate for first 30,000 blocks</p>
</div>
<p>So in a few weeks, the supply will be increasing at a rate of 12.5 ZEC per block, compared to the current rate of 1.2 ZEC per block. This mechanism — the rate of ZEC creation being lower at the beginning — is called Mining Slow Start.</p>
<p>And here is a graph of the total supply over the first couple of months:</p>
<div class="figure align-center" style="width: 75%">
<img alt="Total ZEC distributed for first 30,000 blocks" src="/wp-content/uploads/2016/10/slow-start-total-30k.png"/></p>
<p class="caption">Total ZEC distributed for first 30,000 blocks</p>
</div>
<p>So in a few weeks the total supply will be around 125,000 ZEC, compared to the current supply of 1900 ZEC.</p>
<p>Here is a graph of the total supply over the first half year:</p>
<div class="figure align-center" style="width: 75%">
<img alt="Total ZEC distributed for first 190,000 blocks" src="/wp-content/uploads/2016/10/slow-start-total-190k.png"/></p>
<p class="caption">Total ZEC distributed for first 190,000 blocks</p>
</div>
<p>So in about half a year, the total supply will be around 1,250,000 ZEC.</p>
<p>(Historical note: these graphs are from <a class="reference external" href="/blog/slow-start-and-mining-ecosystem/">our blog post of October 14</a>.)</p>
<hr class="docutils"/>
<p>The first 500 or so blocks came out much faster than one block per two-and-a-half minutes. This is because the amount of mining power that was applied in the first couple of hours was much higher than we anticipated, and the difficulty adjustment algorithm needs a series of time measurements of blocks before it can kick in.</p>
<p>Fortunately, Mining Slow Start means that the first 500 blocks generated only 78 ZEC out of the 1900 ZEC that have been generated so far.</p>
<hr class="docutils"/>
<p>The Founders' Reward (which is going to eventually — after four years — amount to 2,100,000 ZEC) is built into the source code. You can see <a class="reference external" href="https://github.com/zcash/zcash/blob/1feaefac51f64bc51d6954d70dc64b3815f95a05/src/chainparams.cpp#L263">the addresses that the Founders' Reward will be sent to</a>. You can also use the aforementioned block explorer to see the <a class="reference external" href="https://explorer.zcha.in/accounts/t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd">history of the first such address</a>, which (as of the time of this writing) shows that no Zcash has yet been moved out of the Founders' Reward address.</p>
<hr class="docutils"/>
<p>No individual, including me (Zooko), is getting more than 0.5% of the total supply of ZEC, or about 105,000 ZEC, once the entire Founders' Reward has been distributed. (Previously mentioned in our blog post <a class="reference external" href="/blog/continued-funding-and-transparency/">Continued Funding and Transparency</a>.)</p>
<hr class="docutils"/>
<p>Okay, that's the round-up! Stay tuned for more exciting announcements. ☺</p>
