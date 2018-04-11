---
ID: 1660
post_title: >
  How Transactions Between Shielded
  Addresses Work
author: Ariel Gabizon
post_excerpt: ""
layout: post
permalink: >
  https://blog.z.cash/zcash-private-transactions/
published: true
post_date: 2016-11-29 00:00:00
---
In <a class="reference external" href="/blog/anatomy-of-zcash/">'Anatomy of A Zcash Transaction'</a> we gave a general overview of Zcash Transactions. The purpose of this post is to provide a simplified explanation of how <em>privacy-preserving</em> transactions work in Zcash, and where exactly Zero-Knowledge proofs come into the picture. In the terminology of that post, we are focusing exclusively here on transactions between shielded addresses (commonly referred to as z-addrs).

To focus on understanding the privacy-preserving aspect, let's put aside everything having to do with reaching consensus using Proof of Work and the blockchain, and focus on a particular node that has obtained the correct list of unspent transaction outputs.

Let's recall first how this list looks on the bitcoin blockchain. Each unspent transaction output (UTXO) can be thought of as an unspent 'note' that is described by the address/public key of its owner and the amount of BTC it contains. For simplicity of presentation, let's assume each such note contains exactly 1 BTC, and there is at most one note per address. Thus, at a given time, a node's database consists of a list of unspent notes, where each note can be described simply by the address of the owner. For example, the database may look like this.

:math:`\mathsf{Note}_1=` :math:`(\mathsf{PK}_1)`, :math:`\mathsf{Note}_2=` :math:`(\mathsf{PK}_2)`, :math:`\mathsf{Note}_3=` :math:`(\mathsf{PK}_3)`

Suppose :math:`\mathsf{PK}_1` is Alice's address and she wishes to send her 1 BTC note to Bob's address :math:`\mathsf{PK}_4.` She sends a message which essentially says "Move 1 BTC from :math:`\mathsf{PK}_1` to :math:`\mathsf{PK}_4`" to all nodes. She signs this message with the secret key :math:`\mathsf{sk}_1` corresponding to :math:`\mathsf{PK}_1,` and this convinces the node she has the right to move money from :math:`\mathsf{PK}_1.` After the node checks the signature, and checks that there is indeed a 1 BTC note with address :math:`\mathsf{PK}_1,` it will update its database accordingly:

:math:`\mathsf{Note}_4=` :math:`(\mathsf{PK}_4)`, :math:`\mathsf{Note}_2=` :math:`(\mathsf{PK}_2)`, :math:`\mathsf{Note}_3=` :math:`(\mathsf{PK}_3)`

Now suppose each note also contains a random 'serial number' (aka unique identifier) :math:`r.` We will soon see this is helpful for obtaining privacy. Thus, the database may look like this.

:math:`\mathsf{Note}_1=` :math:`(\mathsf{PK}_1,r_1)`, :math:`\mathsf{Note}_2=` :math:`(\mathsf{PK}_1,r_1)`, :math:`\mathsf{Note}_3=` :math:`(\mathsf{PK}_2,r_2)`

A natural first step towards privacy would be to have the node store only "encryptions", or simply hashes, of the notes, rather than the notes themselves.

:math:`\mathsf{H}_1=` :math:`\mathbf{HASH}(\mathsf{Note}_1)`, :math:`\mathsf{H}_2=` :math:`\mathbf{HASH}(\mathsf{Note}_2)`, :math:`\mathsf{H}_3=` :math:`\mathbf{HASH}(\mathsf{Note}_3)`

As a second step to preserve privacy, the node will continue to store the hash of a note <em>even after it has been spent</em>. Thus, it is no longer a database of unspent notes, but rather a database of <em>all notes that ever existed</em>.

The main question now is how to distinguish, without destroying privacy, between notes that have been spent and notes that haven't. This is where the <em>nullifier set</em> comes in. This is a list of hashes of all serial numbers of notes that have been spent. Each node stores the nullifier set, in addition to the set of hashed notes. For example, after :math:`\mathsf{Note}_2` has been spent, the node's database might look like this.
<table class="fixed-table docutils" border="1"><colgroup> <col width="53%" /> <col width="47%" /> </colgroup>
<thead valign="bottom">
<tr>
<th class="head">Hashed notes</th>
<th class="head">Nullifier set</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>:math:`\mathsf{H}_1=` :math:`\mathbf{HASH}(\mathsf{Note}_1)`</td>
<td>:math:`\mathsf{nf}_1=` :math:`\mathbf{HASH}(\mathsf{r}_2)`</td>
</tr>
<tr>
<td>:math:`\mathsf{H}_2=` :math:`\mathbf{HASH}(\mathsf{Note}_2)`</td>
<td></td>
</tr>
<tr>
<td>:math:`\mathsf{H}_3=` :math:`\mathbf{HASH}(\mathsf{Note}_3)`</td>
<td></td>
</tr>
</tbody>
</table>
<h2>How a transaction is made</h2>
Now suppose Alice owns :math:`\mathsf{Note}_1` and wishes to send it to Bob, whose public key is :math:`\mathsf{PK}_4.` We will assume for simplicity that Alice and Bob have a private channel between them although this is not actually necessary in Zcash. Basically, Alice will invalidate her note by publishing its nullifier, and at the same time create a new note that is controlled by Bob.

More precisely, she does the following.
<ol>
 	<li>She randomly chooses a new serial number :math:`r_4` and defines the new note :math:`\mathsf{Note}_4=` :math:`(\mathsf{PK}_4,r_4).`</li>
 	<li>She sends :math:`\mathsf{Note}_4` to Bob privately.</li>
 	<li>She sends the nullifier of :math:`\mathsf{Note}_1,` :math:`\mathsf{nf}_2=` :math:`\mathbf{HASH}(\mathsf{r}_1)` to all nodes.</li>
 	<li>She sends the hash of the new note :math:`\mathsf{H}_4=,` :math:`\mathbf{HASH}(\mathsf{Note}_4)` to all nodes.</li>
</ol>
Now, when a node receives :math:`\mathsf{nf}_2` and :math:`\mathsf{H}_4,` it will check whether the note corresponding to :math:`\mathsf{nf}_2` has already been spent, simply by checking if :math:`\mathsf{nf}_2` already exists in the nullifier set. If it doesn't, the node adds :math:`\mathsf{nf}_2` to the nullifier set and adds :math:`\mathsf{H}_4` to the set of hashed notes; thereby validating the transaction between Alice and Bob.
<table class="fixed-table docutils" border="1"><colgroup> <col width="53%" /> <col width="47%" /> </colgroup>
<thead valign="bottom">
<tr>
<th class="head">Hashed notes</th>
<th class="head">Nullifier set</th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>:math:`\mathsf{H}_1=` :math:`\mathbf{HASH}(\mathsf{Note}_1)`</td>
<td>:math:`\mathsf{nf}_1=` :math:`\mathbf{HASH}(\mathsf{r}_2)`</td>
</tr>
<tr>
<td>:math:`\mathsf{H}_2=` :math:`\mathbf{HASH}(\mathsf{Note}_2)`</td>
<td>:math:`\mathsf{nf}_2=` :math:`\mathbf{HASH}(\mathsf{r}_1)`</td>
</tr>
<tr>
<td>:math:`\mathsf{H}_3=` :math:`\mathbf{HASH}(\mathsf{Note}_3)`</td>
<td></td>
</tr>
<tr>
<td>:math:`\mathsf{H}_4=` :math:`\mathbf{HASH}(\mathsf{Note}_4)`</td>
<td></td>
</tr>
</tbody>
</table>
..but wait a second, we checked that :math:`\mathsf{Note}_1` wasn't spent before.. but we didn't check whether it belongs to Alice. Actually, we didn't check that it was a 'real' note at all, real in the sense that its hash was in the node's table of hashed notes. The simple way to fix this would be for Alice to simply publish :math:`\mathsf{Note}_1,` rather than its hash; but of course, this would undermine the privacy we are trying to achieve.

This is where <em>Zero-Knowledge proofs</em> come to the rescue:

In addition to the steps above, Alice will publish a proof-string :math:`\pi` convincing the nodes that <em>whomever published this transaction knows values</em> :math:`\mathsf{PK}_1,` :math:`\mathsf{sk}_1,` <em>and</em> :math:`r_1` <em>such that</em>
<ol>
 	<li style="list-style-type: none;">
<ol>
 	<li>The hash of the note :math:`\mathsf{Note}_1=` (:math:`\mathsf{PK}_1,` :math:`r_1)` exists in the set of hashed notes.</li>
 	<li>:math:`\mathsf{sk}_1` is the private key corresponding to :math:`\mathsf{PK}_1` (and thus, whomever knows it is the rightful owner of :math:`\mathsf{Note}_1`).</li>
 	<li>The hash of :math:`r_1` is :math:`\mathsf{nf}_2`, (and thus, if :math:`\mathsf{nf}_2` - that we now know is the nullifier of :math:`\mathsf{Note}_1` - is not currently in the nullifier set, :math:`\mathsf{Note}_1` still hasn't been spent).</li>
</ol>
</li>
</ol>
The properties of Zero-Knowledge proofs will ensure no information about :math:`\mathsf{PK}_1,` :math:`\mathsf{sk}_1,` or :math:`r_1` are revealed by :math:`\pi`.
<h3>The main places above where we cheated or omitted details</h3>
We emphasize that this has been an oversimplified description, and recommend the <a class="reference external" href="https://github.com/zcash/zips/blob/master/protocol/protocol.pdf">protocol spec</a> for full details.

Here are some of the main things that were overlooked:
<ol>
 	<li style="list-style-type: none;">
<ol class="arabic simple">
 	<li>The hashed notes need to be stored not just as a list, but in a Merkle tree. This plays an important role in making the Zero-Knowledge proofs efficient. Moreover, we need to store a <em>computationally hiding and binding commitment</em> of the note, rather than just its hash.</li>
 	<li>The nullifier needs to be defined in a slightly more complex way to ensure future privacy of the receiver in relation to the sender.</li>
 	<li>We did not go into details on how to eliminate the need for a private channel between sender and recipient.</li>
</ol>
</li>
</ol>