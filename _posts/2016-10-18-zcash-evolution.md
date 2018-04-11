---
ID: 1652
post_title: Zcash Evolution
author: Nathan Wilcox
post_excerpt: ""
layout: post
permalink: https://blog.z.cash/zcash-evolution/
published: true
post_date: 2016-10-18 00:00:00
---
We are <a class="reference external" href="/announcing-beta-series/">on track to launch</a> the Zcash currency on October 28th. Recently, we shared our vision of Zcash as a <a class="reference external" href="/consensual-currency/">consensual currency</a>: users are always free to run software from whichever developers they choose. Now, before Zcash launches, is a perfect time for us to share some of our visions for how we propose to evolve Zcash.
<div id="upgrade-strategy" class="section">
<h2>Upgrade Strategy</h2>
The most important overarching theme of our future protocol plans is that we intend to deprecate old protocol versions. This will allow us to introduce features that old clients do not recognize, as well as removing old behavior when it's no longer advantageous to retain.

This is sometimes referred to as a <cite>hard forking upgrade</cite> although we prefer to avoid the term <cite>fork</cite> because it's both highly-conflated and often repeated in highly contentious debates. The term <cite>fork</cite> itself can mean at least any of the following:
<ol class="arabic simple">
 	<li>diverging software revisions,</li>
 	<li>persistently diverging blockchain histories,</li>
 	<li>diverging communities.</li>
</ol>
These are orthogonal to each other. For example, a single coherent community may maintain multiple divergent software codebases, or diverging blockchain histories might be supported by a single codebase (e.g. <a class="reference external" href="https://ethcore.io/parity.html">parity</a> after the divergence of <cite>ETH</cite> and <cite>ETC</cite>).

We believe that the protocol upgrades we propose will be acceptable to almost all participants. More importantly, the upgrades will not be unacceptable to a significant population. Whenever this is true, blockchain divergence will be short-lived and the community will continue undivided.

At some point, a proposed upgrade may not be so clearly desired by all participants. Even in this scenario, a proposed upgrade may <em>still</em> provide benefits that outweight the drawbacks (e.g. confusion caused by diverging blockchains). <em>If</em> that's the case, we may still advocate for the upgrade and release software for it. Or, we may decide the risk of a blockchain divergence outweighs the benefit.

One final note about our upgrade strategy: we believe it's possible to have a single coherent Zcash community <em>even if the blockchain diverges</em>, so if we forsee a blockchain divergence, one of our focuses will be in collaborating between the subcommunities participating in each side.

</div>
<div id="potentially-surprising-upgrades" class="section">
<h2>Potentially Surprising Upgrades</h2>
Given that we plan to propose upgrades that will deprecate older protocol implementations, it's important to let people know what kinds of upgrades we plan well in advance, in order to set expectations appropriately. The following examples are not comprehensive, nor are they the coolest or most exciting upgrades on our radar. Rather they are a selection of upgrades we expect will surprise some fraction of potential users, and are thus the most important to communicate before Zcash launches.
<div id="mining" class="section">
<h3>Mining</h3>
We already intend to alter our mining system, at the very least by altering the Equihash parameters. In the future we may even advocate more drastic changes, such as moving to a different proof-of-work system or even proof-of-stake, if we believe those alternatives are feasible, secure, and have better economic effects.

</div>
<div id="founders-reward" class="section">
<h3>Founders' Reward</h3>
If the Founders' Reward were to suffer a severe flaw or if our keys were stolen or compromised, we would advocate an upgrade to repair the damage.

</div>
<div id="counterfeit-detection" class="section">
<h3>Counterfeit Detection</h3>
Any currency with strong privacy carries a risk of undetected counterfeiting <a id="id1" class="footnote-reference" href="/zcash-evolution#id3">[1]</a>. For any security system, a crucial complement to prevention is detection. We've started sketching out several potential protocol upgrades for counterfeit detection. These will allow all users to potentially detect, and in some cases to limit, counterfeiting due to security breakthroughs.

Some of the counterfeit detection schemes we've considered rely on expiring old, abandoned funds (i.e. users might need to take action to ensure that their dormant funds are not flagged as expired).

</div>
<div id="removing-technical-debt" class="section">
<h3>Removing Technical Debt</h3>
Zcash is derived from the Bitcoin Core code and design. We chose this implementation path in order to benefit from a battle-tested, conservative design and codebase. Because we will be proposing upgrades which deprecate features, we will have the opportunity to remove technical debt when it seems safe and beneficial to do so <a id="id2" class="footnote-reference" href="/zcash-evolution#id4">[2]</a>.

</div>
<div id="and-more" class="section">
<h3>…and More</h3>
As mentioned earlier, this list is not comprehensive. We may advocate for other upgrades which may surprise some users, which aren't listed here. The ideas above are merely what we consider fairly likely and the most "surprising" potential upgrades. And remember, these aren't the <em>coolest</em> potential upgrades. ;-)

</div>
</div>
<div id="future-evolution" class="section">
<h2>Future Evolution</h2>
We've presented here a taste of the kinds of upgrades we may advocate for in the future. Keep in mind, we also plan to change our technical strategy appropriately as Zcash grows.

For example, if the userbase remains relatively small with a few niche use cases, we may promote more rapid evolution of features. However, if Zcash were to grow to many stakeholders encompassing many different use cases, this would imply the design at that time was already successful at supporting economic weight, and we would likely adopt a more conservative strategy.

One final thought: we've discussed here and in the <a class="reference external" href="/consensual-currency/">consensual currency</a> post how we intend to propose changes that anyone is free to adopt, but we haven't yet clarified <em>how</em> proposals will be made, what the decision process will look like, and how we'll solicit input from stakeholders. That's a topic for another post.

—Nathan Wilcox, 2016-10-18

<strong>Footnotes:</strong>
<table id="id3" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="/zcash-evolution#id1">[1]</a></td>
<td>Different privacy systems have different <cite>attack surfaces</cite> which, if compromised, lead to counterfeiting. For Zcash the attack surfaces include the initial parameter setup, the security assumptions supporting soundness of zk-SNARK proofs, and the zk-SNARK circuit construction that maintains the currency balance rules for shielded transactions. When analyzing fungible currency systems, it is important to determine the attack surface for counterfeiting vulnerability.</td>
</tr>
</tbody>
</table>
<table id="id4" class="docutils footnote" frame="void" rules="none"><colgroup><col class="label" /><col /></colgroup>
<tbody valign="top">
<tr>
<td class="label"><a class="fn-backref" href="/zcash-evolution#id2">[2]</a></td>
<td>The Bitcoin community maintains <a class="reference external" href="https://en.bitcoin.it/wiki/Hardfork_Wishlist">a wishlist</a> for just this purpose. We have the opportunity to test these clean-ups in our live network so that Bitcoin community can learn from our successes and mistakes.</td>
</tr>
</tbody>
</table>
</div>