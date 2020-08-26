---
ID: 4890
post_title: History of Hash Function Attacks
post_name: hash-functions
post_date: 2017-02-24 00:00:00
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/hash-functions/
published: true
tags:
  - BLAKE2
  - cryptography
  - hash functions
categories:
  - General
---
<p>The SHA-1 hash function, which has long been considered insecure, is now <a class="reference external" href="https://security.googleblog.com/2017/02/announcing-first-sha1-collision.html">officially broken</a> as of yesterday. Given the renewed interest in hash function collisions, I'd like to point out an article I wrote about attacks on secure hash functions, in the hopes that you will find it useful and interesting.</p>
<p>You can can read the full article at <a class="reference external" href="https://z.cash/technology/history-of-hash-function-attacks.html">https://z.cash/technology/history-of-hash-function-attacks.html</a>.</p>
<p>The main result of this investigation is that a cryptosystem invulnerable to collision attacks is much safer than one that is vulnerable to collision attacks (regardless of whether it is vulnerable to pre-image attacks). Another interesting takeaway is that it looks like sometime between 1996 (Tiger) and 2000 (Whirlpool), humanity might have<br />
learned how to make collision-resistant hash functions, since none of the prominent secure hash functions designed since that era have succumbed to collision attacks. Maybe modern hash functions like SHA-256, SHA-3, and BLAKE2 will never be broken.</p>
<p>As a graphical reference for the article, I've included a color-coded chronological view of collision attacks, and of second pre-image attacks, as well as a survey of the best known attacks on secure hash functions.</p>
<div class="figure align-center">
<a class="reference external image-reference" href="https://z.cash/technology/history-of-hash-function-attacks.html"><img alt="chronological view of collision attacks" class="center-image" src="/wp-content/uploads/2017/02/hash-functions-chronology.png"/></a>
</div>
<p>Thanks to Andreas Hülsing, Samuel Neves, and Zcash engineer Daira Hopwood for their input on this investigation.</p>
