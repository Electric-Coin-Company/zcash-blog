---
ID: 4884
post_title: 'Founders&#8217; Reward Transfers'
post_name: founders-reward-transfers
post_date: 2016-11-15 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/founders-reward-transfers/
published: true
tags:
  - "Founders' Reward"
  - mining
  - Transparency
categories:
  - General
---
<p>With the Zcash launch of October 28th, 2016, a couple weeks behind us, and a couple of bugfix releases out, we're beginning to turn our focus to the coming year. The last lingering task to complete our MVP goal is to begin the Founders' Reward transfers.</p>
<p>We will begin initiating transfers of the Founders' Reward funds sometime on or after November 28th, 2016, a month after our launch. Recipients of the Founders' Reward may independently use these funds as they see fit. Additionally the end of the <cite>mining slow start</cite> is predicted to be roughly around the same time after which the rate of ⓩ production over time will become constant for approximately the following four years.</p>

<div class="section" id="background">
<h2>Background</h2>
<p>The rest of this post presents a technical background on the <cite>Founders' Reward</cite> and the <cite>Miners' Reward</cite>, and how the <cite>mining slow start</cite> interacts with them. Finally, some of the links provided allow you to observe up-to-date details for these kinds of funds.</p>
<p>For further background, please see our prior blog posts:</p>
<ul class="simple">
<li><a class="reference external" href="/blog/funding/">Funding</a></li>
<li><a class="reference external" href="/blog/continued-funding-and-transparency/">Continued Funding and Transparency</a></li>
<li><a class="reference external" href="/blog/slow-start-and-mining-ecosystem/">User Expectations at Sprout Pt. 1: Slow-Start Mining &amp; Mining Ecosystem</a></li>
</ul>
</div>

<div class="section" id="monetary-base-and-founders-reward">
<h3>Monetary Base and Founders' Reward</h3>
<p>The Founders' Reward is the cornerstone of our funding and developer incentives model, and allocates 10% of <em>all</em> tokens created to a Founders' Reward fund, with the remaining 90% allocated to miners eventually.</p>
<p class="figure align-center" style="width: 75%">
<img alt="Zcash Distribution" class="zecc-blog-inline-image" src="/wp-content/uploads/2016/09/founders-reward-1-v3.png"/></p>
<p class="caption">Source: <a class="reference external" href="/blog/continued-funding-and-transparency/">Continued Funding and Transparency</a></p>
<p>The 10% of the total supply that makes up the Founders' Reward is distributed between launch and the first halving (at block 850,000). During this period (which will last approximately four years), half of the total monetary base will be generated. After the first halving, there will be no more Founders' Reward, and all newly-created ⓩ will be received by miners. The following figure shows the monetary base and Founders' Reward plotted over time:</p>
<p class="figure align-center" style="width: 75%">
<img alt="Founders Reward Graph" class="zecc-blog-inline-image" src="/wp-content/uploads/2016/11/foundersreward.png"/></p>
<p class="caption">Source: <a class="reference external" href="/blog/funding/">Funding</a></p>
</div>

<div class="section" id="block-subsidies">
<h3>Block Subsidies</h3>
<p>When a new valid block is discovered, the special <cite>coinbase</cite> transaction is permitted to create new ⓩ tokens according to the monetary base growth schedule. The <em>total</em> number of ⓩ created per block in this beginning stage of the network follow the <cite>slow start</cite> rule: for the first 20,000 blocks, the number of ⓩ grows linearly from 0 ⓩ towards 12.5 ⓩ (which is approximately ~34 days). Thus the 20,000th block is the first block with a 12.5 ⓩ subsidy. As of this writing we are around block 11034, or about 55% through the slow-start period. This figure shows the rate per block as a function of block height:</p>
<p class="figure align-center" style="width: 85%">
<img alt="ZEC distribution rate for first 30,000 blocks" src="/wp-content/uploads/2016/11/slow-start-rate-30k.png"/></p>
<p class="caption">ZEC distribution rate for first 30,000 blocks. Source: <a class="reference external" href="/blog/slow-start-and-mining-ecosystem/">User Expectations at Sprout Pt. 1: Slow-Start Mining &amp; Mining Ecosystem</a></p>
<p>This block subsidy is split between the Miners' Reward (80%) and the Founders' Reward (20%) during the halving interval. After that the entire block subsidy will go to the Miners' Reward. You can see an example by viewing any <cite>coinbase transaction</cite>, such as <a class="reference external" href="https://explorer.zcha.in/transactions/ad1f2885b082e1990c3b843876ecdc3d8f4a3be9bd31ea7f980f9dda081ef645">this example from block 8086</a>:</p>
<ul class="simple">
<li>Address <tt class="docutils literal">t1XepX38RxS3o5hLioLbaNb6Fa2Y2Be55xw</tt>, the miner's address, receives 4.0431 ⓩ, and</li>
<li>Address <tt class="docutils literal">t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd</tt>, which collects the Founders' Reward, receives 1.01075 ⓩ.</li>
</ul>
</div>

<div class="section" id="founders-reward-addresses">
<h3>Founders' Reward Addresses</h3>
<p>The miner's address is chosen by the miner at the time they created the block, whereas the founders' Reward address, <a class="reference external" href="https://explorer.zcha.in/accounts/t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd">t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd</a> seen above, is specified in the consensus rules (specifically in <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0/src/chainparams.cpp#L135-L192">this source code</a>). Throughout the approximately four years of Founders' Reward distribution, the specific addresses used will change, a measure to improve our operational security.</p>
<p>You can see that as of this writing (around block 8775), no funds have moved from the Founders' Reward address <a class="reference external" href="https://explorer.zcha.in/accounts/t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd">t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd</a> (link to <a class="reference external" href="https://explorer.zcha.in/">zcha.in explorer</a>). Once we begin transfering funds out of that address, the URL should reflect those transfers out.</p>
</div>

<div class="section" id="conclusion">
<h2>Conclusion</h2>
<p>Once Founders' Reward transfers begin, on or around November 28th, and the <cite>slow start</cite> completes the Zcash network will be in the basic post-launch steady state. We designed the Founders' Reward as the best practical structure to make Zcash a reality, both in its launch and it's continued evolution. We're avidly preparing for that evolution!</p>
</div>

<div class="section" id="resources">
<h3>Resources</h3>
<p>To learn about the current public state of Founders' Reward funds or Miners' reward funds, you can use the following resources:</p>
<ul class="simple">
<li>The list of all Founders' Reward addresses is found in <a class="reference external" href="https://github.com/zcash/zcash/blob/v1.0.0/src/chainparams.cpp#L135-L192">this source code</a> table.</li>
<li>The untransfered balance of the Founders' Reward can be viewed with any 'balance view' of those addresses, such as this view of the current <a class="reference external" href="https://explorer.zcha.in/accounts/t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd">t3Vz22vK5z2LcKEdg16Yv4FFneEL1zg9ojd</a> address.</li>
<li>The rewards for the Miner and Founders are found in any <cite>coinbase</cite> transaction, such as <a class="reference external" href="https://explorer.zcha.in/transactions/ad1f2885b082e1990c3b843876ecdc3d8f4a3be9bd31ea7f980f9dda081ef645">this example from block 8086</a>.</li>
</ul>
<p>Note: The last two links are to the <a class="reference external" href="https://explorer.zcha.in/">zcha.in explorer</a> which is not operated by the Zcash Company. Any blockchain explorer will provide the same information.</p>
</div>