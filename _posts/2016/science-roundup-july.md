---
ID: 4936
post_title: Science Roundup
post_name: science-roundup-july
post_date: 2016-07-27 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/science-roundup-july/
published: true
tags:
  - BOLT
  - Science Roundup
  - security
categories:
  - General
---
<p>Zcash is a science-driven company, and our team is always working on advancing the forefront of human knowledge. Here is a round-up of science news from our team.</p>
<h2>Side Channel Attacks on Everyday Applications</h2>
<p>Zcasher Taylor Hornby will be presenting on <a class="reference external" href="https://www.blackhat.com/us-16/briefings.html#side-channel-attacks-on-everyday-applications">Side Channel Attacks on Everyday Applications</a> at the Black Hat conference on August 3.</p>
<p>In this talk, Taylor will briefly describe how the FLUSH+RELOAD attack works, and how it can be used to build input distinguishing attacks. In particular, he’ll demonstrate how when the user Alice browses around the top 100 Wikipedia pages, the user Bob can spy on which of those pages she's visiting. This isn't an earth-shattering attack, but as the code he’ll release shows, it can be implemented reliably. The goal is to convince the community that side channels, FLUSH+RELOAD in particular, are useful for more than just breaking cryptography.</p>
<p>Known for his carefully written security tools, including a side-channel-free password generator and a cryptography library for PHP, Taylor regularly contributes to a number of open-source projects by security auditing and reviewing source code. This work builds on the foundations laid in part by Zcash scientist Eran Tromer (<a class="reference external" href="http://cs.tau.ac.il/~tromer/cache/">http://cs.tau.ac.il/~tromer/cache/</a>).</p>
<p>The event is in Las Vegas, USA from July 30-Aug 4, 2016. Full info here: <a class="reference external" href="https://www.blackhat.com/us-16/">https://www.blackhat.com/us-16/</a></p>
<h2>Image Authentication</h2>
<p>Zcash scientist, Eran Tromer, presents an application of SNARKs in the area of image authentication.</p>
<p>Authenticity of digital photographs is important in many contexts, including social websites, dating, news reporting, and legal evidence. In principle, authenticity could be ensured by secure in-camera signing of images, as offered by some cameras. However, users often need to apply some legitimate editing operations to images (e.g., cropping, downscaling and brightness adjustment), in order to prepare them for publication. Creating an image authentication scheme that allows some editing operations, but not others, has been a subject of active research for decades.</p>
<p>Eran and his student have created a new image authentication scheme, PhotoProof, which is the first to allow complete flexibility in the choice of what editing operations are permissible, and is also more robust to forgery. The scheme is based on the same zero-knowledge SNARK proof systems that underlie Zcash. Whereas Zcash reasons about the provenance of digital currency across payment operations, PhotoProof reasons about the provenance of images across editing operations.</p>
<p>There is more information about this here: <a class="reference external" href="https://cs.tau.ac.il/~tromer/photoproof/">https://cs.tau.ac.il/~tromer/photoproof/</a></p>
<h2>Lawsuit on DMCA Section 1201: Research &amp; Technology Restrictions Violate 1st Amendment</h2>
<p>The Electronic Frontier Foundation (EFF) is suing the U.S. government on behalf of technology creators and researchers to overturn onerous provisions of copyright law that violate the First Amendment, as stated in <a class="reference external" href="https://www.eff.org/press/releases/eff-lawsuit-takes-dmca-section-1201-research-and-technology-restrictions-violate">this blog post</a>.</p>
<p>Zcasher Matthew Green is a plaintiff in the trial “who wants to make sure that we all can trust the devices that we count on to communicate, underpin our financial transactions, and secure our most private medical information. Despite this work being vital for all of our safety, Green had to seek an exemption from the Library of Congress last year for his security research.”</p>
<h2>Blind Off-Chain Lightweight Transactions</h2>
<p>Matthew Green and Ian Miers, two of the seven founders/scientists of the Zcash company, have a paper on BOLT (Blind Off-chain Lightweight Transactions). It’s roughly a privacy preserving version of payment channels like Lightning for Zcash. We will be publishing a more in-depth blog post about it early next week.</p>
<p>Private payment channels are important because they allow you to pay someone without waiting for block confirmation and they greatly reduce the volume of transactions that must be recorded in the blockchain. Payment channels work by creating blockchain-backed IOUs between two parties, which they can then update without using the blockchain to reflect the balance of funds between them. But this process isn’t private since the IOU serves as a unique identifier the merchant can use to link multiple payments together. So for example, if you are using a payment channel to pay for page views on a website, it’s effectively a tracking cookie.</p>
<p>BOLT uses blind signatures and commitments to make private IOUs. When you present one to a merchant, these record the fact that the merchant’s balance in the IOU has increased, but without actually revealing which IOU it is you are using and thus who you are. BOLT even supports payments via an intermediary when there is no direct channel between two parties. And the intermediary learns nothing, not even the amount that is paid.</p>
<h2>Towards Trapdoor-Free Zero Knowledge Proving Systems</h2>
<p>The strong privacy guarantees of Zcash are made possible by significant computer science breakthroughs from the last few years. These breakthroughs circumvent the use of Probabilistically Checkable Proofs (PCPs).</p>
<p>PCPs are a powerful theoretical computer science tool, and until recently were considered essential for efficient Zero-Knowledge proof systems. The reason for wanting to avoid the use of PCPs is that although they are efficient from a theoretical standpoint, they are considered notoriously inefficient and too complex in practice.</p>
<p>This avoidance comes at a cost: in these new systems there is always trapdoor information that should be destroyed after the system is initialized, and which could compromise the system if ever discovered.</p>
<p>In <a class="reference external" href="https://eprint.iacr.org/2016/646">a recent work</a>, SCIPR Lab has made a significant first step towards making PCP-based systems, in which no such trapdoor exists, closer to practice. Currently they are able to generate proofs about programs that use a million machine cycles. The <a class="reference external" href="http://www.scipr-lab.org/team.html">team working on this</a> includes five Zcashers: Eli Ben-Sasson, Alessandro Chiesa, Ariel Gabizon, Eran Tromer and Madars Virza.</p>
<h2>Ciphertext Attacks on iMessage</h2>
<p>The Washington Post published the story: "<a class="reference external" href="https://www.washingtonpost.com/world/national-security/johns-hopkins-researchers-discovered-encryption-flaw-in-apples-imessage/2016/03/20/a323f9a0-eca7-11e5-a6f3-21ccdbc5f74e_story.html">Johns Hopkins researchers poke a hole in Apple’s encryption</a>," which describes the results of research that Zcashers Matthew Green, Ian Miers, and Christina Garman (along with others) have been working on over the past few months. Below is part of Matthew Green’s blog post to describe the research and implications. For more technical reading, the academic paper can be found here: “<a class="reference external" href="https://isi.jhu.edu/~mgreen/imessage.pdf">Dancing on the Lip of the Volcano: Chosen Ciphertext Attacks on Apple iMessage.</a>”</p>
<p>From Matthew Green’s blog post (<a class="reference external" href="http://blog.cryptographyengineering.com/2016/03/attack-of-week-apple-imessage.html">full text here</a>)...<br />
“As you might have guessed from the headline, the work concerns Apple, and specifically Apple's iMessage text messaging protocol. Over the past months my students Christina Garman, Ian Miers, Gabe Kaptchuk and Mike Rushanan and I have been looking closely at the encryption used by iMessage, in order to determine how the system fares against sophisticated attackers. The results of this analysis include some very neat new attacks that allow us to –under very specific circumstances– decrypt the contents of iMessage attachments, such as photos and videos.”</p>
<div class="figure align-center">
<img alt="iMessage research team" class="blog-imessage-research-team" src="/wp-content/uploads/2016/07/imessage-research-team.png"></div>
<p>The research team. From left: Gabe Kaptchuk, Mike Rushanan, Ian Miers, Christina Garman</p>
<p>Connect to the Zcash conversation by <a class="reference external" href="https://inviteme.z.cash/">joining our Slack channel</a> or get infrequent email notifications by <a class="reference external" href="https://z.cash/zh/#launch-notification">signing up</a>.</p>
