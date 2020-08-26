---
ID: 4961
post_title: The Design of the Ceremony
post_name: the-design-of-the-ceremony
post_date: 2016-10-26 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/the-design-of-the-ceremony/
published: true
tags:
  - launch
  - Parameter Generation
  - zkSNARKs
categories:
  - General
---
<p>Update: <a class="reference external" href="https://z.cash/technology/paramgen.html">Read our full summary</a> of what took place in the Zcash Parameter Generation Ceremony.</p>
<div class="section" id="the-toxic-waste-and-other-ways-to-counterfeit-zcash">
<h2>The Toxic Waste, and Other Ways To Counterfeit Zcash</h2>
<p>As we've mentioned in a <a class="reference external" href="/blog/snark-parameters/">previous blog post</a>, the private transactions in Zcash “Sprout” 1.0 rely on <em>SNARK public parameters</em> for constructing and verifying zero-knowledge proofs. (When we upgrade the Zcash protocol and change the zero-knowledge proofs — which we intend to do within about a year — then we'll have to generate new SNARK public parameters from scratch.) Generating SNARK public parameters is basically equivalent to generating a public/private keypair, keeping the public key, and destroying the private key.</p>
<p>The problem is, if an attacker were to get a copy of that corresponding private key, they could use it to create counterfeit Zcash. That is the <em>only</em> harm they could do with it — they could not violate anyone else's privacy nor steal other people's Zcash.</p>
<p>We call the private key “the toxic waste”, and our protocol is designed to ensure that the toxic waste never comes into existence at all. Imagine having a bunch of different chemical byproducts in your factory, each of which is individually harmless, but if you let <em>all</em> of them mix together they will form a dangerous substance that's difficult to manage safely. Our approach is to keep the individually-harmless chemicals separate until they are destroyed, so the toxic waste never comes into existence at all.</p>
<p>Important note: destroying the private key doesn't guarantee that it's impossible to counterfeit Zcash! Every currency technology ever made has been vulnerable to counterfeiting. Bitcoin once had a bug which allowed the first person who discovered it to <a class="reference external" href="https://en.bitcoin.it/wiki/Value_overflow_incident">counterfeit 184 billion BTC</a>. Zcash could turn out to have a similar flaw, totally unrelated to the toxic waste private key.</p>
<p>Bitcoin was able to detect this problem because it publicly exposes all transactions. Zcash won't have that ability. In fact, <em>any</em> system which shields the amounts of transactions risks losing the ability to detect such counterfeiting.</p>
<p>Zcash is not unique in the risk that it could be counterfeited, nor in the difficulty of detecting counterfeiting. We'll return to this fact at the end of this post.</p>
</div>
<div class="section" id="the-design-of-a-secure-ceremony">
<h2>The Design of a Secure Ceremony</h2>
<p>In order to reduce the risk of an attacker acquiring the toxic waste, we developed a <a class="reference external" href="/blog/generating-zcash-parameters/">Multi-Party Computation</a> (MPC) protocol in which a set of multiple participants in separate geographic locations cooperatively construct the public key. Each participant separately generates one <em>shard</em> of the public key, which requires them to temporarily use a corresponding private key shard. They all combine their public key shards to generate the final public parameters, and then each deletes their private key shard.</p>
<p>With the MPC protocol, as long as <em>at least one</em> of the participants successfully deletes their private key shard, then the toxic waste is impossible for anyone to reconstruct. The only way the toxic waste can be reconstructed is if <em>every</em> participant in the protocol were dishonest or compromised.</p>
<p>I myself, plus five people who I trust to be ethical and to have good information security practices, served as the operators and observers in the protocol. We call these people “Witnesses”, and we call the execution of the protocol a “Ceremony”.</p>
<p>The identities of three of the Witnesses were revealed to all of the participants and observers at the beginning of the Ceremony: Andrew Miller (<a class="reference external" href="http://soc1024.ece.illinois.edu/">computer scientist</a> and <a class="reference external" href="https://z.cash/team.html#advisors">Zcash technical advisor</a>), <a class="reference external" href="http://www.petervv.com/">Peter Van Valkenburgh</a>, and yours truly.</p>
<p>I told these participants that their fellow witnesses were named “Moses Spears”, “Fabrice Renault”, and “John Dobbertin”, but in fact I made up those pseudonyms in order to temporarily hide the identities of those other Witnesses. I did this in order to hide their identities from any potential attacker who was able to eavesdrop on our (mostly encrypted) communications or to subvert one of our other Witnesses.</p>
<p>At the end of the Ceremony, on October 23, “Moses Spears” was revealed to be Derek Hinch of NCC Group. We had secretly hired NCC Group to be one of the Compute Node operators. Nobody other than Nathan Wilcox (ZcashCo CTO), myself, and NCC Group knew about this. NCC Group's task was both to protect their Compute Node during the ceremony (they hosted it in their secure facility in Austin), and to do forensic analysis during and after the Ceremony in order to attempt to detect whether there had been any cyber attack attempted against it. Additionally, they set up a redundant model Compute Node that wasn't used in the actual Ceremony, and attempted to hack into it to see how hard it would be for a Witness to steal the private key shard out of a Compute Node. NCC Group will write a tech report about what they did and observed.</p>
<p>On October 27, “Fabrice Renault” <a class="reference external" href="https://twitter.com/petertoddbtc/status/791495928108625921">revealed himself</a> to be Bitcoin Core developer Peter Todd. Peter had expressed skepticism about the Zcash Parameter Generation Ceremony, and I told him that serving as a Witness would give him the best vantage point from which to scrutinize and criticize it. Most importantly, I trust that Peter would never collude to attempt to steal the private key shards. Finally, I guessed that he would deploy creative and strong information security defenses. I do not yet know the details of those defenses, since he has not yet posted his report. We didn't pay Peter to do this, although we did agree to reimburse his expenses, such as buying a new computer from a random store and then a couple of days later completely destroying it.</p>
<p>The identity of “John Dobbertin” has not yet been revealed, and I don't yet know when John and I will be ready to do that.</p>
<p>Several of the Witnesses made photo, video, and/or audio recordings of the process, and we invited a journalist to observe one of the stations — Denver Station, where I was located. We'll publish these records as soon as we've organized, labeled, and hosted them and scanned for any private and personal information that we may have accidentally captured.</p>
<p>The Ceremony design we chose has three core defenses which work together: <em>Multi-Party Computation</em>, <em>air gaps</em>, and <em>evidence trails</em>.</p>
<div class="section" id="id1">
<h3>Multi-Party Computation</h3>
<p>The <em>Multi-Party Computation</em> effect is that it only takes <em>one</em> of these people to successfully delete their private key shard for us to succeed. As soon as any one of the Witnesses deleted their private key shard, then the toxic waste could never be created. This is the starting point of our design, and it dovetails well with the other defenses.</p>
</div>
<div class="section" id="air-gaps">
<h3>Air Gaps</h3>
<p>Each participant's private key shard was used solely on an air-gapped machine. <em>Air-gapping</em> means that the computer is physically disconnected from all networks.</p>
<p>Each machine was bought new, exclusively for this purpose, and was never connected to any network during its entire life, from the moment that it was purchased at the store by the Witness. The Witness physically removed the radios (wifi and bluetooth) from the computer before first powering it on.</p>
<p>These air-gapped machines were called the “Compute Nodes”.</p>
<p>The air gap eliminated most of the attack surface that could allow an attacker to compromise the Compute Nodes, since the Compute Nodes were physically incapable of making or receiving network connections.</p>
<p><img alt="an air-gapped Compute Node being set up" class="zecc-blog-inline-image" src="/wp-content/uploads/2016/10/compute-node.jpg"/></div>
<div class="section" id="evidence-trails">
<h3>Evidence Trails</h3>
<p>We needed to communicate messages back and forth between the Compute Nodes in order to perform the Multi-Party Computation protocol.</p>
<p>Each Witness had, in addition to the Compute Node, a separate machine which was connected to the Internet, which we called the “Network Node”. The Network Node received incoming messages and burned them to disc, and then the Witness moved the disc across the air gap to the Compute Node.</p>
<p>This replaced the attack surface that we had removed — networking — with a different attack surface — DVD reading. We hope that the new attack surface was harder to exploit, but it is difficult to be sure about such things. For example, if you could have put maliciously crafted data onto the discs (i.e. if you had already compromised the Network Node), then it may have been possible to exploit the Compute Node's DVD reader's firmware, or it may have been possible to exploit the userspace code on the Compute Node that read the messages.</p>
<p>A major advantage of using append-only optical discs is that they provide an indelible <em>evidence trail</em> of exactly what messages were passed during a particular Ceremony. For example, suppose that in the future someone discovers that there was an exploitable bug in the firmware of the DVD device that was used in one of the Compute Nodes. We can then ask: well, <em>did</em> the messages that were fed into that Compute Node exploit that bug? We can inspect the optical discs to see if any data were passed into the Compute Node that might have exploited such a vulnerability.</p>
<p>It is important that the optical discs are not overwriteable — they are DVD-R's, not DVD-RW's — because that way even if an attacker succeeded at taking over the Compute Node, that wouldn't have given them the ability to erase the evidence of them doing so.</p>
<p><img alt="ceremony design" class="zecc-blog-inline-image" src="/wp-content/uploads/2016/10/paramgen_v3.png"/></div>
</div>
<div class="section" id="additional-defenses">
<h2>Additional Defenses</h2>
<p>In addition to the triad of core defenses outlined above, we also used numerous additional techniques to make our jobs as defenders easier and to make any potential attacker's task harder. We kept the details of the Ceremony — when it was going to be executed, who the participants would be, what source code we would run, etc. — secret until after the Ceremony had been completed — until now! We used a security-hardened version of Linux on the Compute Nodes. We wrote all of the code we needed for the computation and the networking in Rust — a programming language which makes it easy to avoid writing the most common security bugs. We made a secure hash chain of all the messages that were passed, and we posted that hash chain <a class="reference external" href="https://twitter.com/zooko/status/789894254021660673">to Twitter</a> and <a class="reference external" href="https://web.archive.org/web/20161022182123/https:/twitter.com/zooko/status/789894254021660673">the Internet Archive</a>, and time-stamped it into the Bitcoin blockchain. In addition, each of the Witnesses chose their own additional local defenses, which we will describe in more detail in future documents.</p>
</div>
<div class="section" id="future-work">
<h2>Future Work</h2>
<p>Our task is not yet done. Here are two important steps to take next:</p>
<div class="section" id="evidence-archiving-and-independent-inspection">
<h3>Evidence Archiving and Independent Inspection</h3>
<p>We will write more documentation explaining the details of the protocol and the Ceremony, including who the Witnesses were, when and where (six different locations!) the Ceremony was held, and extensive details about the process. We'll publish the video, audio, photographic, and textual evidence that we recorded. We are also asking each of the Witnesses to write an attestation about what they did and what they observed. We are working hard on writing, publishing, and archiving all of this material so that anyone can inspect it.</p>
<p>I think that this material will prove extremely interesting to our fellow paranoid infosec experts. I look forward to hearing their evaluation of our security precautions and what we observed during the execution of the Ceremony. As far as I know, the Zcash Parameter Generation Ceremony is the most remarkable and sophisticated cryptographic ceremony that has ever been executed!</p>
<p>We have already begun this process by publishing <a class="reference external" href="https://github.com/zcash/mpc/tree/c2012297b01a72c63505053b2c79ad33159141f5">the source code</a> of the network process and the computation process. Please read it and let us know right away if you find any exploitable flaws in it.</p>
</div>
<div class="section" id="a-proposed-counterfeiting-detection-feature-for-zcash">
<h3>A Proposed Counterfeiting-Detection Feature for Zcash</h3>
<p>Although we are currently satisfied that the toxic waste private key corresponding to these Zcash 1.0 public parameters never came into existence, and can never come into existence, I am <em>not</em> sure that counterfeiting Zcash is impossible. This is because, as I wrote above, there may be other ways to create counterfeit Zcash coins besides reconstructing the toxic waste private key.</p>
<p>Also, people who did not have the opportunity to witness the Ceremony first-hand may still have doubts that it was executed honestly and safely. There is no way that we can actually prove that we really did what we said we did. We could have all six colluded to perform the whole process — making video footage and all — as a stage-magic trick, and we could have <em>actually</em> secretly copied the private key shards and combined them to form the toxic waste. I chose the other five Witnesses to be people who I personally trusted never to do such a thing, but if you don't know these people as I do, then you may require additional safeguards.</p>
<p>Therefore, I intend to advocate for a Zcash protocol upgrade in the future — after the launch of Zcash 1.0 “Sprout” — which adds a <em>counterfeiting-detection</em> feature. This will provide a way for anyone (i.e. the general public) to measure the total monetary base of Zcash coins in circulation. This will allow us to determine whether counterfeiting — whether by exploiting the toxic waste private key or by any other mechanism — has occurred.</p>
<p>I will write more on this in a future blog post.</p>
</div>
</div>
<div class="section" id="the-bottom-line">
<h2>The Bottom Line</h2>
<p>We have performed a remarkable feat of cryptographic and infosec engineering in order to generate SNARK public parameters for Zcash 1.0 “Sprout”. The general design of this Ceremony was based on Multi-Party Computation, air-gaps, and indelible evidence trails. Six different people each took one part of the Ceremony. The Multi-Party Computation ensures that even if all five of the <em>others</em> were compromised, or were secretly colluding, to try to reconstruct the toxic waste, one single Witness behaving honestly and deleting their shard of the toxic waste would prevent it from ever being reconstructable. Despite the remarkable strength of this Ceremony, I intend to advocate for a major upgrade to the Zcash protocol next year which will add a layer of <em>detection</em> in addition to the current layer of <em>prevention</em>.</p>
</div>
