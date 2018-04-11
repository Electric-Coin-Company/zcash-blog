---
ID: 1551
post_title: >
  Celebrating the Zcash Developer
  Community
author: Paige Peterson
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/community-projects/
published: true
post_date: 2017-09-01 00:00:00
---
<p>Since <a class="reference external" href="/zcash-begins/">the launch</a> of Zcash about 10 months ago, we've seen a promising selection of support from a variety of third-party developers. New and existing businesses have adopted Zcash into their <a class="reference external" href="https://www.zcashcommunity.com/wallets/">wallet</a> and <a class="reference external" href="https://www.zcashcommunity.com/markets/">exchange</a> platforms which has helped to create a strong start for the ecosystem.</p>
<p>However, in this post we'd like to celebrate another set of third-party developers who contribute not just to the ecosystem but also as part of the community. You'll find these community developers in the <a class="reference external" href="https://chat.zcashcommunity.com">chat</a> and <a class="reference external" href="https://forum.z.cash">forum</a> discussing new ideas, connecting with collaborators and sharing the projects they've been building and experimenting on.</p>
<p>These open source community projects are the heart of the Zcash ecosystem. They include ports of the <a class="reference external" href="https://z.cash/download.html">official Zcash client</a> which support other operating systems, a messaging platform which leverages the shielded address encrypted memo field and  a private, decentralized storage network that uses Zcash for payments. Most of the development for these projects is fueled by a love to create interesting and useful tools and donations from the community. While many are experimental in nature, we look forward to their continued maturation and evolution.</p>
<p>So without futher ado, let's look at some of the interesting development work brought to you by the talented developers in the Zcash community.</p>
<div class="section" id="zchain">
<h2>Zchain</h2>
<p><a class="reference external" href="https://explorer.zcha.in">Zchain</a> developed and maintained by <a class="reference external" href="https://forum.z.cash/u/lustro">lustro</a>, is the first Zcash block explorer. It was released during the first days of the Zcash blockchain and continues to be a vital resource for transaction data details and usage statistics. It also provides an API for developers to interact with transparent blockchain data.</p>
<div class="figure align-center">
<a class="reference external image-reference" href="https://network.zcha.in/"><img alt="Zchain network map (Asia)" class="center-image" src="http://blog.z.cash/wp-content/uploads/2017/09/zcash-globe-asiaaustralia-sm.png"/></a>
</div>
<p>The <a class="reference external" href="https://network.zcha.in/">network map</a> on Zchain is another useful tool showing stats and a beautiful visualization of nodes connected to the Zcash network.</p>
</div>
<div class="section" id="insight-for-zcash">
<h2>Insight for Zcash</h2>
<p><a class="reference external" href="https://zcashnetwork.info/">Insight</a> is another blockchain explorer based on the bitcore library originally built for Bitcoin and was forked for the Zcash blockchain. It is helpful as a redundant resource for users searching for transparent Zcash transaction data and for web app developers interested in building Zcash services. This explorer is maintained by community developer <a class="reference external" href="https://github.com/radix42/">radix42</a>.</p>
</div>
<div class="section" id="zcash-vanity">
<h2>zcash-vanity</h2>
<p>The <a class="reference external" href="https://zcash.plutomonkey.com/vanity/">zcash-vanity</a> tool is a Zcash vanity address generator for shielded addresses written in Rust and maintained by <a class="reference external" href="https://zcash.plutomonkey.com/">PlutoMonkey</a>. It is high-throughput and can run on GPU devices for faster address discovery.</p>
</div>
<div class="section" id="vanitygen-z">
<h2>vanitygen_z</h2>
<p>The <a class="reference external" href="https://github.com/exploitagency/vanitygen_z">vanitygen_z</a> tool is a vanity address generator for Zcash transparent addresses by community developers <a class="reference external" href="https://github.com/exploitagency">exploitagency</a> and <a class="reference external" href="https://github.com/Voluntary-zcash">Voluntary</a>. It is a fork of the vanitygen tool built for Bitcoin and works for standard (<cite>t1...</cite>) and multi-sig (<cite>t3...</cite>) addresses. This implementation includes further modification to support GPU devices.</p>
</div>
<div class="section" id="zcash-mini">
<h2>zcash-mini</h2>
<p>The <a class="reference external" href="https://github.com/FiloSottile/zcash-mini">zcash-mini</a> tool by <a class="reference external" href="https://github.com/zmanian">zmanian</a> and <a class="reference external" href="https://github.com/FiloSottile">FiloSottile</a> is a minimal portable Zcash shielded address generator for offline and paper wallets. It also offers a vanity address generator and the ability to create shielded Zcash addresses with associated mnemonic strings.</p>
</div>
<div class="section" id="zcash4win-zcash4mac-swing-wallet">
<h2>zcash4win &amp; zcash4mac &amp; Swing Wallet</h2>
<p>The two earliest ports of the <a class="reference external" href="https://z.cash/download.html">official Zcash client</a> are <a class="reference external" href="https://zcash4win.com/">zcash4win</a> and <a class="reference external" href="https://zcash4mac.com/">zcash4mac</a>. We featured these applications in the <a class="reference external" href="https://www.youtube.com/watch?v=wk6qsqGGXSs">first episode of our Show &amp; Tell series</a> where the developer, <a class="reference external" href="https://github.com/radix42/">radix42</a>, walks through the features of the software. Both are GUI desktop clients forked from <a class="reference external" href="https://github.com/vaklinov/zcash-swing-wallet-ui">Swing Wallet</a> which is a separately maintained GUI wrapper for Zcash command line clients by <a class="reference external" href="https://github.com/vaklinov">vaklinov</a>.</p>
<div class="figure align-center">
<img alt="Screenshot of Zcash Swing Wallet UI" class="center-image high-res-image" src="http://blog.z.cash/wp-content/uploads/2017/09/SwingWallet.png"/></div>
</div>
<div class="section" id="zcash-apple">
<h2>Zcash Apple</h2>
<p>Another project to support macOS is <a class="reference external" href="https://github.com/kozyilmaz/zcash-apple">Zcash Apple</a> by <a class="reference external" href="https://github.com/kozyilmaz">kozyilmaz</a>. While it only provides command line tools, it is also compatible with the <a class="reference external" href="https://github.com/vaklinov/zcash-swing-wallet-ui">Swing Wallet</a> GUI software. As of now, it is kept more up-to-date than the zcash4mac software but installing requires building the software from source. Instructions for doing so are provided in the documentation.</p>
</div>
<div class="section" id="pyzcto-zcash-pannel">
<h2>Pyzcto &amp; Zcash Pannel</h2>
<p><a class="reference external" href="https://github.com/miguelmarco/pyzcto">Pyzcto</a> is an alternative UI built for the <a class="reference external" href="https://z.cash/download.html">official Zcash client</a>. It additionally allows users to set up an Onion service on the Tor network which can be used with the <a class="reference external" href="https://github.com/miguelmarco/ZcashPannel">Zcash Pannel</a> Android application. The Android app gives users the option of managing the Linux Zcash client from your phone connecting through Tor for added privacy. This pair of projects is maintained by community developer <a class="reference external" href="https://github.com/miguelmarco">miguelmarco</a>.</p>
</div>
<div class="section" id="zmsg">
<h2>zmsg</h2>
<p>An interesting piece of software called <a class="reference external" href="https://github.com/whyrusleeping/zmsg">zmsg</a> leverages the encrypted memo field of Zcash shielded transactions to send messages to others. We featured the developer of zmsg, <a class="reference external" href="https://github.com/whyrusleeping">whyrusleeping</a> on the <a class="reference external" href="https://www.youtube.com/watch?v=HVqk6We2Das">second episode of our Show &amp; Tell series</a>.</p>
</div>
<div class="section" id="orc">
<h2>ORC</h2>
<p>And last but not least, a new project called <a class="reference external" href="https://orc.network/">ORC</a> leverages Tor and Kademlia routing to create a private, peer-to-peer object storage platform. The project has plans to integrate Zcash for payments to incentivise network nodes to host content. The <a class="reference external" href="https://github.com/orcproject">ORC Project</a> consists of a small team of open source developers.</p>
</div>
<div class="section" id="and-more">
<h2>And more...</h2>
<p>These projects are just a selection of the interesting and exciting tools the Zcash community has been building since the launch of Zcash last October. We encourage Zcash users to support these projects by trying them out, providing feedback and donating to the developers. As we mentioned, most of these projects are still in an experimental phase so please be cautious when trusting them with your money.</p>
<p>The <a class="reference external" href="https://z.cash.foundation">Zcash Foundation</a> has recently announced their first <a class="reference external" href="https://z.cash.foundation//blog/grant-program/">grant program</a> which community developers looking for financial assistance should certainly consider applying for to support underserved public services in the Zcash ecosystem. We also encourage all developers to share their ideas in the community <a class="reference external" href="https://chat.zcashcommunity.com">chat</a> and official <a class="reference external" href="https://forum.z.cash">forum</a>.</p>