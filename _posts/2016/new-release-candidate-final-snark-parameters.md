---
ID: 4922
post_title: 'New Release Candidate: Final zk-SNARK parameters'
post_name: >
  new-release-candidate-final-snark-parameters
post_date: 2016-10-27 00:00:00
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/new-release-candidate-final-snark-parameters/
published: true
tags:
  - Parameter Generation
  - releases
  - sprout
  - zkSNARKs
categories:
  - General
---
<p>The Zcash team has been working to finalize the software for the launch of the Zcash blockchain. We are planning to make the launch release available on the morning (PDT) of 28th October, subject to any last-minute technical hitches.</p>
<p>Over last weekend the final zk-SNARK parameters were created in the <a class="reference external" href="/blog/the-design-of-the-ceremony/">Parameter Generation Ceremony</a>. The <a class="reference external" href="https://github.com/zcash/mpc">transcripts and software used for the ceremony</a> have been published, and we'll be making another post with more information on that very soon.</p>
<p>We encourage everyone to test this latest <tt class="docutils literal"><span class="pre">1.0.0-rc4</span></tt> release by following the <a class="reference external" href="https://github.com/zcash/zcash/wiki/Public-Beta-Guide">Beta Guide</a>. That will also make sure that you are able to run the software on your system, and have the zk-SNARK parameters (a ~910 MB download) ready for launch.</p>
<div id="two-releases" class="section">
<h2>Two Releases</h2>
<p>As part of a strategy to reduce technical risk and to ensure auditability, we have made two releases within a day of each other. Most users should skip from <tt class="docutils literal"><span class="pre">1.0.0-rc2</span></tt> directly to <a class="reference external" href="https://github.com/zcash/zcash/milestone/44?closed=1">1.0.0-rc4</a>.</p>
<div id="rc3-bug-fixes-and-dependency-upgrades" class="section">
<h3>1.0.0-rc3 - bug fixes and dependency upgrades</h3>
<p>The intermediate <a class="reference external" href="https://github.com/zcash/zcash/milestone/43?closed=1">1.0.0-rc3</a> release included only bug fixes, and updates of libraries that Zcash depends on:</p>
<ol class="arabic simple">
<li>The node metrics screen added in the rc2 release caused a bug when the output was not directed to a terminal, which has been corrected. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1612">#1612</a>)</li>
<li>The version of Berkeley DB has been updated to 6.2.23. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1637">#1637</a>)</li>
<li>The tinyformat library was updated in order to mitigate a potential buffer overflow vulnerability. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1640">#1640</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1349">#1349</a>)</li>
<li>A fix for a minor potential race condition was backported from Bitcoin. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1634">#1634</a>)</li>
<li>A couple of portability problems with the <cite>fetch-params.sh</cite> script and the Debian packages have been fixed. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1053">#1053</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1537">#1537</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1613">#1613</a>)</li>
<li>We have eliminated an error-prone case and a confusing error message when spending part of a coinbase output (e.g. mining reward). As a consequence it is now necessary to spend coinbase outputs exactly so that there is no change; the node will not implicitly select a change address. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1616">#1616</a>)</li>
<li>Updates to documentation and examples. (<a class="reference external" href="https://github.com/zcash/zcash/pull/826">#826</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/965">#965</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1152">#1152</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1154">#1154</a>, <a class="reference external" href="https://github.com/zcash/zcash/pull/1643">#1643</a>)</li>
<li>Network bootstrapping for mainnet. (<a class="reference external" href="https://github.com/zcash/zcash/pull/1369">#1369</a>)</li>
</ol>
</div>
<div id="rc4-zksnark-params-and-founders-reward-addresses" class="section">
<h3>1.0.0-rc4 - zkSNARK Params and Founders' Reward Addresses</h3>
<p>The <a class="reference external" href="https://github.com/zcash/zcash/milestone/44?closed=1">1.0.0-rc4</a> release, which is the one now deployed on the testnet, made some final updates in preparation for the Zcash launch:</p>
<ol class="arabic simple">
<li>The zk-SNARK parameters have been updated to the ones created by the ceremony performed last weekend.</li>
<li>The <a class="reference external" href="/blog/continued-funding-and-transparency/">Founders' Reward</a> addresses for mainnet have also been updated.</li>
</ol>
<p>For a more complete list of changes, see our <a class="reference external" href="https://github.com/zcash/zcash/milestone/43?closed=1">1.0.0-rc3</a> and <a class="reference external" href="https://github.com/zcash/zcash/milestone/44?closed=1">1.0.0-rc4</a> release github milestones.</p>
</div>
</div>
<div id="imminent-launch" class="section">
<h2>Imminent Launch</h2>
<p>In the remaining time before launch, we will only make further changes if they are necessary to correct critical problems that would be an obstacle to Zcash launching successfully. If all goes to plan, the only thing remaining is the mainnet genesis block — the code is done!</p>
<p>It takes some time to generate the genesis block, and build the binaries. We're going to mint the genesis block and prepare binaries etc. the night before (i.e. this evening, Thursday, Oct 27), and then go to sleep. Then we will get up and release it the next morning, San Francisco time. Keep an eye on our <a class="reference external" href="https://twitter.com/electriccoinco">Twitter feed</a>!</p>
<p>To follow our progress, watch <a class="reference external" href="https://github.com/zcash/zcash/milestones">the GitHub project</a> and <a class="reference external" href="https://forum.z.cash/">join the forum</a>. To get an email announcement when <a class="reference external" href="/blog/sprout-roadmap/">Zcash Sprout</a> is ready, put your email address <a class="reference external" href="https://z.cash/#launch-notification">in here</a>.</p>
</div>
