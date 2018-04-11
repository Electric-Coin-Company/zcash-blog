---
ID: 1557
post_title: Deterministic Builds in Zcash
author: Kevin Gallagher
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/deterministic-builds/
published: true
post_date: 2016-10-17 00:00:00
---
<p>As Mike Perry of Tor Project <a class="reference external" href="https://blog.torproject.org/blog/deterministic-builds-part-one-cyberwar-and-global-compromise">wrote back in 2013</a>, while the Snowden revelations were ongoing, one of the most dreaded of scenarios is the so-called “watering hole" attack, where an adversary or malware <em>“attacks the software development and build processes themselves to distribute copies of itself to tens or even hundreds of millions of machines in a single, officially signed, instantaneous update.”</em></p>
<p>Though the world hasn’t witnessed many such attacks yet, the Zcash blockchain and its user base could be considered a prime target, both since they might have an interest in retaining control over their own privacy, and because it’s expected that ZEC will acquire real-world monetary value.</p>
<p>We're keen on presenting verifiably secure and trustworthy software to the world, as demonstrated by the <a class="reference external" href="/auditing-zcash/">several audits</a> we've commissioned. So for our version 1.0.0 release candidates, we have started following a deterministic build process, courtesy of Gitian.</p>
<p><a class="reference external" href="https://gitian.org/">Gitian</a> is a method of secure software distribution which allows multiple developers to create identical binaries. It was originally developed by <a class="reference external" href="https://bitcoin.org/en/">Bitcoin Core</a>, and was subsequently adapted for use by the <a class="reference external" href="https://www.torproject.org/">Tor Project</a>. Cryptographic signatures and hashes are leveraged in order to ensure that the toolchain was not tampered with, and the same, official source was used to make the binaries that are eventually released.</p>

<h2>How it works</h2>
<p>In Gitian, you have a list containing a number of inputs, which all have hashes associated with them. These are the Zcash source code, its third-party dependencies, and the OS packages. There are also obvious outputs: the Zcash binaries, which will soon be available via a public apt package repository for Debian-based distributions. For each release, we have multiple people from our project build the binaries within a contained environment, and then sign the results with their GPG key, attesting to the inputs they used and the outputs that were generated. The manifest of hashes and corresponding signatures is then <a class="reference external" href="https://github.com/zcash/gitian.sigs">published on GitHub</a> and compared with the others. If there is any difference present, then we will be aware that the inputs have been modified in some way, either maliciously or not.</p>
<p>We will never release a binary that was not built deterministically. We are also architecting a sophisticated security regime around protecting the master signing key used to verify downloads from our origins.</p>
<p>The most common source of indeterminism in software is timestamps. Therefore, during this whole process, timestamps and other metadata are either stripped from files, or various wrappers are used to make timestamps correspond to a reference date and time. This usually results in a build that is reproducible by anyone.</p>
<p>By way of illustration, when we first started using Gitian, we uncovered a single source of irreproducibility in libsnark, the library we use for zero-knowledge proving. Two of our developers compared their outputs and found a mismatch:</p>
<dl class="docutils"><dt>::</dt>
<dd>-    1edeaed33a85eef3e190160e781d3b0cc6e389eda53c382ccc555241fa0e1e51  x86_64-unknown-linux-gnu/libsnark/libsnark-0.1-a97aa3c0de8.tar.gz
+    cec7ca83f5767d8553891906953ffbe38935ecbc379971b6cb7e449467495c00  x86_64-unknown-linux-gnu/libsnark/libsnark-0.1-a97aa3c0de8.tar.gz</dd>
</dl><p>Drilling down into the diff, we found that the binary forms of the library differed. Using a tool called diffoscope, we discovered that there were timestamps encoded in the binary:</p>
<dl class="docutils"><dt>::</dt>
<dd>$ diffoscope libsnark-0.1-a97aa3c0de8.tar.gz libsnark-0.1-a97aa3c0de8.tar.gz.2
--- libsnark-0.1-a97aa3c0de8.tar.gz
+++ libsnark-0.1-a97aa3c0de8.tar.gz.2
├── libsnark-0.1-a97aa3c0de8.tar
│   ├── ./lib/libsnark.a
│   │   │ @@ -51,16 +51,16 @@
│   │   │ -  [    74]  21:08:27
│   │   │ -  [    7d]  Oct 15 2016
│   │   │ +  [    74]  03:30:18
│   │   │ +  [    7d]  Oct 16 2016
│   │   ╵
│   ╵</dd>
</dl><p>We quickly traced it to <a class="reference external" href="https://github.com/scipr-lab/libsnark/blob/master/src/common/profiling.cpp#L346-L351">this function</a>, which prints the date and time of compilation, and developed a <a class="reference external" href="https://github.com/zcash/libsnark/pull/7">fix</a>.</p>
<p>We think that having deterministic builds is an exciting milestone for Zcash, and encourage other open-source projects to follow suit.</p>

<h2>Technical details</h2>
<p>The <a class="reference external" href="https://github.com/zcash/zcash-gitian">Zcash deterministic build environment</a>, which runs Debian 8, is a virtual machine created with <a class="reference external" href="https://www.vagrantup.com/">Vagrant</a>, using <a class="reference external" href="https://www.virtualbox.org/">VirtualBox</a> for virtualization. It runs <a class="reference external" href="https://github.com/devrandom/gitian-builder">gitian-builder</a> and Linux containers (LXC) as guests.</p>
<p><a class="reference external" href="https://docs.ansible.com/ansible/index.html">Ansible</a>, a Python-based configuration management tool, is used to provision the initial environment. The script which interacts with gitian-builder, itself a Ruby-based tool, is written in Bash. Much of our tooling borrows from the fine work already done by Bitcoin Core, but we have automated away many of the steps required to bootstrap the system.</p>
<p>We welcome anyone who is technically inclined and enthusiastic about Zcash to help us produce more builds. If you’re interested, contact us on our <a class="reference external" href="https://inviteme.z.cash/">community Slack</a> #zcash-dev channel.</p>