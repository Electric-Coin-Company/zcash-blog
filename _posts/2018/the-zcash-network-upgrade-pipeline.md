---
ID: 5745
post_title: The Zcash Network Upgrade Pipeline
post_name: the-zcash-network-upgrade-pipeline
post_date: 2018-12-03 13:50:50
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/the-zcash-network-upgrade-pipeline/
published: true
tags:
  - network upgrade
  - pipeline
categories:
  - Technical
---
<!-- wp:paragraph -->
<p>With the successful <a href="/blog/sapling-activation-complete/">activation of Sapling</a>, the Zcash Company engineering team is focused on two strategic priorities in 2019: facilitating the adoption of a <em>shielded standard</em> throughout the ecosystem and, designing and implementing our next <em>protocol upgrade</em>—dubbed <em>Zcash Blossom</em>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We’re in the early phases of defining the technical goals for Blossom, which we plan to activate in October of 2019. If you’re eager to dig into those feature goals, I recommend reading my forum post, <a href="https://forum.zcashcommunity.com/t/announcing-zcash-blossom-and-proposed-feature-goals/31891" target="_blank" rel="noreferrer noopener" aria-label="We’re in the early phases of defining the technical goals for Blossom, which we plan to activate in October of 2019. If you’re eager to dig into those feature goals, I recommend reading my forum post, Announcing Zcash Blossom and proposed feature goals. (opens in a new tab)">Announcing Zcash Blossom and proposed feature goals</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For this post, I’d like to focus on the <em>process</em> we’re using to safely ship new protocol upgrades in Zcash, which we call the <em>Zcash Network Upgrade Pipeline</em>. We’ve developed this process to meet a variety of goals, based on everything we’ve learned from the Zcash launch and the Overwinter and Sapling upgrades. The primary goals are to <strong>ship safely</strong><strong>—</strong>with plenty of time for <strong>ecosystem partner integration</strong>, in <strong>collaboration across multiple organizations</strong><strong>—</strong>in a <strong>governance agnostic manner</strong>, all while <strong>pipelining concurrent upgrades</strong>. &nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>The Pipeline at a Glance</h2>
<!-- /wp:heading -->

<!-- wp:image {"id":5784,"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2018/11/Network-Upgrade-Pipeline-v1.0-1.png" target="_blank" rel="noreferrer noopener"><img src="https://dev-electriccoinco-wordpress.pantheonsite.io/wp-content/uploads/2018/11/Network-Upgrade-Pipeline-v1.0-1-1024x459.png" alt="" class="wp-image-5784"/></a><figcaption><strong>Note: We will skip the April 2019 <em>Upgrade A</em> slot shown on the diagram as described later in this post.</strong></figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>The Network Upgrade Pipeline defines a scheduled sequence of <em>coordination points</em> to bring consensus features from the speculative realm down into the production Zcash network.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This process is time-based and designed to ensure the consensus upgrades shipped to Zcash meet our historic standards for safety and quality. It is intended to support the development of multiple subsequent upgrades concurrently, thus the term “pipeline.” The Zcash Company aims to set a consistent pace of two upgrades per year, indicated as <em>Upgrade A</em> and <em>Upgrade B</em> in the diagram.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The coordination points, represented by red-outlined diamonds in this chart, signify essential, high-level milestones that must be fulfilled for a given feature set to ship on-time, in every case embodied as a <em>deliverable.</em> These milestones represent “input points” for protocol changes for the Company, the Foundation and the wider community. If someone from the Foundation or community wants to submit a change to Zcash that requires a network upgrade, they need to ensure their <a href="https://github.com/zcash/zips" target="_blank" rel="noreferrer noopener" aria-label="The coordination points, represented by red-outlined diamonds in this chart, signify essential, high-level milestones that must be fulfilled for a given feature set to ship on-time, in every case embodied as a deliverable. These milestones represent “input points” for protocol changes for the Company, the Foundation and the wider community. If someone from the Foundation or community wants to submit a change to Zcash that requires a network upgrade, they need to ensure their ZIPs hit each of these milestones. (opens in a new tab)">ZIPs</a> hit each of these milestones.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The colors and vertical separation for different phases distinguishes a division of roles. Many of these coordination points involve a hand-off from a <em>submitting role</em> to an <em>accepting role</em>. For example, an <em>R&amp;D Lead</em> delivers a set of <em>feature requirements</em> to a <em>Specification Lead</em>. For these hand-offs, it’s the responsibility of the accepting role to ensure the deliverable meets the requirements before proceeding with their subsequent responsibility.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We intend to simplify the logistics of collaboration across development teams by clarifying these roles, the deliverables, the hand-offs, and which role has the ability to ensure the process is on-track and meets our quality standards.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Open Collaboration and Evolving Governance</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The Network Upgrade Pipeline is an execution process, not a governance or evaluation process. It doesn’t define how decisions are made, although it does clarify roles for making “execution decisions,” such as if a proposed specification meets the criteria to begin implementation and design audits.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We believe that by nailing down the execution process, we can clarify and simplify the much harder and crucial concerns of decision making, governance, and stakeholdership. The Zcash Company is following this process for the Blossom upgrade while collaborating with development teams outside the company. We’ll share more as those collaborations develop.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We anticipate the Network Upgrade Pipeline will work well while running continuously, even while governance evolves across the Zcash ecosystem.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><br><em>Note (2019-05-21): Please check out the <a rel="noreferrer noopener" aria-label="Network Update Pipeline v1.1 (opens in a new tab)" href="https://docs.google.com/drawings/d/1WAvIkVBv_fC4L4wDoAJaMTYVh3dJbwhR5YuP5HgOjFw/edit" target="_blank">Network Update Pipeline v1.1</a> for more up-to-date information.</em></p>
<!-- /wp:paragraph -->