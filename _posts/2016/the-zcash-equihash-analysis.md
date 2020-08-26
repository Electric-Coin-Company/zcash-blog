---
ID: 4963
post_title: The Zcash Equihash Analysis
post_name: the-zcash-equihash-analysis
post_date: 2016-11-18 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/the-zcash-equihash-analysis/
published: true
tags:
  - Equihash
  - mining
  - security
  - security audits
categories:
  - General
---
<p>As we <a class="reference external" href="/blog/auditing-zcash/">announced</a> back in August, we commissioned two security audits of the Zcash codebase and an analysis of our proof-of-work algorithm. We <a class="reference external" href="/blog/audit-results/">published</a> the two security audits shortly before Zcash’s launch. Today, we are pleased to share the analysis from <a class="reference external" href="https://en.wikipedia.org/wiki/Solar_Designer">Solar Designer</a> of the Zcash Equihash proof-of-work scheme.</p>
<h2>Solar Designer’s Report</h2>
<p><strong>Report URL:</strong> <a class="reference external" href="http://www.openwall.com/articles/Zcash-Equihash-Analysis">http://www.openwall.com/articles/Zcash-Equihash-Analysis</a></p>
<dl class="docutils">
<dt><strong>Solar’s summary:</strong></dt>
<dd>
<p class="first">“I was tasked with analyzing Zcash’s choice and use of the Equihash proof-of-work scheme, including its potential for future optimizations on both commodity and custom hardware. Also in-scope were the choice of and potential changes to Equihash parameters that Zcash uses.</p>
<p class="last">“A conclusion is that while Equihash is not among the most ASIC-resistant known PoW schemes, its choice by Zcash may pose a reasonable tradeoff considering Zcash’s multiple goals and depending on which properties of the PoW turn out to be actually most important to users of Zcash. Another conclusion is that Zcash’s current n=200, k=9 Equihash parameters are suboptimal and may need to be changed.”</p>
</dd>
</dl>
<h2>Related Work</h2>
<p>In addition to the analysis presented here, Solar Designer is one of three judges evaluating the first <a class="reference external" href="https://zcashminers.org/">Zcash Mining Competition</a>, which we announced <a class="reference external" href="/blog/announcing-miner-contest/">previously on this blog</a>.</p>
<p>The Zcash Company dev team and community are using this analysis, the mining competition, and input from the community to inform potential future proposals to change the consensus protocol. If you’re interested in contributing please join the <a class="reference external" href="https://chat.zcashcommunity.com/channel/zcash-miner-dev"><tt class="docutils literal"><span class="pre">#zcash-miner-dev</span></tt></a> community chat channel.</p>
<p>To keep up in general with the Zcash Company, read this blog, follow our <a class="reference external" href="https://twitter.com/electriccoinco">@electriccoinco</a> Twitter handle, and join our forum.</p>
