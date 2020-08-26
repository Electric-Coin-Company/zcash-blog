---
ID: 4953
post_title: 'User Expectations at Sprout Pt. 2: Software Usability and Hardware Requirements'
post_name: >
  software-usability-and-hardware-requirements
post_date: 2016-10-19 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/software-usability-and-hardware-requirements/
published: true
tags:
  - launch
  - sprout
  - users
categories:
  - General
---
<p>This is the second post in a two-part series about what users can expect from the launch of Zcash Sprout. The <a class="reference external" href="/blog/slow-start-and-mining-ecosystem/">first post</a> highlighted the effects of the slow-start mining period on the market, and accessibility to the overall mining ecosystem. Accessibility for Zcash end users, whether they participate in the mining ecosystem or not, is a critical aspect within the overall Zcash mission. While this initial release comes relatively limited in its mainstream usability, we anticipate core improvements and tools built by third-party developers (such as wallets with graphical interfaces and integrations with exchanges) in the days and months following the launch creating many more opportunities for Zcash users. In the meantime, early adopters should be aware of initial limitations and set expectations appropriately during the budding phase of Sprout.</p>
<div class="section" id="using-linux-natively-or-through-a-virtual-environment">
<h2>Using Linux natively or through a virtual environment</h2>
<p>Whether experienced with using the command-line install process, or simply curious to try, we encourage you to install Zcash Sprout on a Debian or Ubuntu based system (you can get a head start with the current <a class="reference external" href="https://github.com/zcash/zcash/wiki/Beta-Guide">Beta release</a>). Users running other operating systems are similarly encouraged to run a Debian or Ubuntu based virtual environment for the install. We will have written and video documentation to walk you through the command-line instructions for a Debian package install (which is supported by Ubuntu). While we can’t officially give support to users on setting up a virtual environment, we can recommend looking into <a class="reference external" href="https://www.virtualbox.org/">VirtualBox</a> - and together with community support from the <a class="reference external" href="https://forum.z.cash/">Zcash community</a> and <a class="reference external" href="https://forums.virtualbox.org/">VirtualBox forums</a>, there’s plenty of opportunity to receive guidance along the way.</p>
</div>
<div class="section" id="blockchain-and-zero-knowledge-proof-generation-hardware-requirements">
<h2>Blockchain and zero-knowledge proof generation hardware requirements</h2>
<p>The other half of accessibility considerations involves the optimal resources for running a Zcash node. First, it’s important to reiterate Zcash is a blockchain. While the storage requirements at first will be relatively low, the growth of the ledger is something to plan for. With a block size maximum of 2MB and average block time of 2.5 minutes, the maximum growth of the blockchain after one year is 420 GB. We don't anticipate blocks filling to their maximum (especially in this first year) and we cannot predict what the average blocksize will be but it's safe to assume that with increased adoption, the rate of growth for the Zcash blockchain will also increase.</p>
<p>Additionally, the process of creating transactions involving zero-knowledge proofs will occupy 4 GB of RAM for about a minute or two. While we hope to see improvements on this metric in future versions, this will be an important aspect of planning to send ZEC to a shielded address at launch. Sending ZEC using transparent addresses does not involve generating a zero-knowledge proof and requires very little memory (comparable to sending a bitcoin transaction).</p>
<p>On installing the Beta release (and again upgrading to Beta 2) on my own laptop which I restricted to 4 GB of memory for testing purposes, I had to shut down nearly every process while the zero-knowledge proof was generated for a testnet transaction. While I was successful, it was definitely pushing the upper limits and took almost 2 minutes to complete the operation. So if your computer has only 4 GB in available memory, you might want to consider upgrading. If your computer has less than that, you’ll be limited to transparent transactions unless you upgrade to at least 4 GB (preferably more).</p>
<p>The current state of zero-knowledge proof generation represents an initial implementation. Optimization is an <a class="reference external" href="https://github.com/zcash/zcash/issues/750">open task</a> within the core development roadmap, and centers around removing unnecessarily stored data throughout the proof generation process. There is no prediction yet for how much reduction in memory is possible, but we should have a better idea once additional research has been performed.</p>
<p>Overall, it has taken a lot of hard work to get to Sprout and it will take a lot more to get where we want to go. We encourage the Zcash community to experiment with us, and if you have the means, to prepare your system for the resource requirements. Use the <a class="reference external" href="https://forum.z.cash/">Zcash community forum</a> to discuss your findings, ideas, and work with others on support needs. Your active participation only makes this network stronger.</p>
</div>
