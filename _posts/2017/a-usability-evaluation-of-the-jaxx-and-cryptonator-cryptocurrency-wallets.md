---
ID: 7661
post_title: >
  A usability evaluation of the Jaxx and
  Cryptonator cryptocurrency wallets
post_name: >
  a-usability-evaluation-of-the-jaxx-and-cryptonator-cryptocurrency-wallets
post_date: 2017-08-21 18:00:06
layout: post
link: >
  https://dev-electriccoinco-wordpress.pantheonsite.io/blog/a-usability-evaluation-of-the-jaxx-and-cryptonator-cryptocurrency-wallets/
published: true
tags: [ ]
categories:
  - General
---
<p><!-- wp:html --></p>
<div class="subtitle"><i class="fa fa-link" aria-hidden="true"></i>
<div class="subtitle-text">
<h2 id="summary">Summary</h2>
</div>
</div>
<p>A cryptocurrency wallet (or crypto wallet) enables users to feasibly send, receive, and monitor their digital currency by storing private and public keys and interacting with various blockchain components. If you want to use Zcash or any other cryptocurrency, you will need to have a digital wallet.</p>
<p>We recommend both Jaxx and Cryptonator as great crypto wallet options. The reason why we evaluated Jaxx and Cryptonator is because we wanted to make them even better. Most crypto wallets are in early phases of implementation and adoption, so we suspect that any issues found here with Jaxx and Cryptonator are likely present in other crypto wallets as well. If you’re a developer for another crypto wallet, we recommend reading this case study, and checking that these issues are addressed in your wallet!</p>
<p>Both crypto wallets enable the user to send, receive, and exchange Zcash in an intuitive way. We found that Jaxx (v. 1.2.17) onboards its users well and is easy to setup and use, but is missing some user feedback when transactions fail. Cryptonator (v. 2.0.3) has lots of security measures such as email verification, device verification, and PIN, but this makes it hard to set up and navigate.</p>
<div class="subtitle"><i class="fa fa-link" aria-hidden="true"></i>
<div class="subtitle-text">
<h2 id="evaluation-testing">Evaluation and testing</h2>
</div>
</div>
<p>We first examined the application and its interface from a user experience designer’s standpoint, and give out evaluation of each screen:</p>
<table class="table table-responsive">
<thead>
<tr>
<th scope="col">Screen</th>
<th scope="col">Cryptonator</th>
<th scope="col">Jaxx</th>
</tr>
</thead>
<tbody>
<tr>
<th scope="row">Landing screen</th>
<td class="yellow">It shows you a list of your wallets and your balances (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_ZV81SVhkX2RVdWc" target="_blank" rel="noopener noreferrer">image</a>). To send transactions, you need to go back a couple screens and find the appropriate menu.</td>
<td class="green">It sends you to one of your wallets directly, and shows your balance, transactions, and allows you to send and receive transactions in one click. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_b0NxWnlSQTNPbjg" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Send payment screen</th>
<td class="green">Intuitive UI, showing all the necessary fields.(<a href="https://drive.google.com/open?id=0B36YkvDtVNK_NXhjMnJhNXU5NUk" target="_blank" rel="noopener noreferrer">image</a>)</td>
<td class="green">Intuitive UI, showing all the necessary fields.(<a href="https://drive.google.com/open?id=0B36YkvDtVNK_X2F2QkR5MVdubUk" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Request payment screen</th>
<td class="yellow">N/A</td>
<td class="green">Allows you to copy your address, or input an amount to generate a QR code (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_eU8zY240ckNLbnM" target="_blank" rel="noopener noreferrer">image</a>), a sample QR code that encodes address and send amount. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_dUtEYXNqRGl3dVU" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Exchange payment screen</th>
<td class="red">Not screenshot-able, but it looks okay--similar looking to the send payment screen. Doesn’t show the conversion rate or fees associated with this action.</td>
<td class="green">Intuitive UI, showing conversion rates, and minimum and maximum exchange values. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_RnpLaHV3cE9XeGs" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Sent transaction details</th>
<td class="green">Has information about the transaction and provides a space to annotate what the transaction is for.</td>
<td class="yellow">Has the information you need, but no space for annotations. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_Znc0a1I5S3NKU2M" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Received transaction details</th>
<td class="green">Has information about the transaction and provides a space to annotate what the transaction is for. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_NXp3ZEstWjQ5MWs" target="_blank" rel="noopener noreferrer">image</a>)</td>
<td class="yellow">Has the information you need, but no space for annotations. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_QlZ1amh2RkFXR00" target="_blank" rel="noopener noreferrer">image</a>)</td>
</tr>
<tr>
<th scope="row">Transaction fee details</th>
<td class="green">Transaction fees are listed as a separate transaction, but has minimal information about the fee. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_OGxkYWhaaXM4d0U" target="_blank" rel="noopener noreferrer">image</a>)</td>
<td class="green">Transaction fee details are included in the sent transaction and not separately, which reduces visual clutter.</td>
</tr>
</tbody>
</table>
<p>We tested how easy it was to complete certain tasks, assuming a first time user who is trying their best to complete the task correctly:</p>
<table class="table table-responsive">
<thead>
<tr>
<th scope="col">Task</th>
<th scope="col">Cryptonator</th>
<th scope="col">Jaxx</th>
</tr>
</thead>
<tbody>
<tr>
<th scope="row">Installation and setup</th>
<td class="dark-red">Requires a signup account and too many user tasks--plus it was hard to verify email, account, set up pin, etc. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_ZWgyZ2MtNlU1Wkk" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="dark-green">Near flawless! Minimal options, easy, and quick. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_WW1vVERGdWRFY3c" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Sending payment</th>
<td class="green">Easy to find where it is, and can send payments easily. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_RU1HZ2I3bXhZUXc" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="green">Easy to find where it is, and can send payments easily. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_Znc0a1I5S3NKU2M" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Receiving payment</th>
<td class="red">No push notification that a transaction was received (although there is for sending one) and no notification in app--just a balance update. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_elF0RHhxU05ET3c" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">No push notification of receiving payment, no in-app notification of receiving payment--just a balance update. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_RTlBV2F3RTNKVWM" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Exchanging currencies</th>
<td class="yellow">Relatively easy to exchange (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_VUx0VHpWang5eUE" target="_blank" rel="noopener noreferrer">video</a>), but if you miss the leading zero in a small number (.02 rather than 0.02), it errors out. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_UjZSdlhRRW1JdkU" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">It was unclear that you could exchange payment if you didn’t know what shapeshift was (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_LUswSmVsZUEzREk" target="_blank" rel="noopener noreferrer">video</a>, <a href="https://drive.google.com/open?id=0B36YkvDtVNK_ckl3VzVVc3M4M0U" target="_blank" rel="noopener noreferrer">video</a>, <a href="https://drive.google.com/open?id=0B36YkvDtVNK_djA1ZlcyNU56a28" target="_blank" rel="noopener noreferrer">video</a>), but otherwise okay. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_TWE5OHY5VkJhSkk" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
</tbody>
</table>
<p>Since we also wanted to see how the crypto wallets respond to users who are not successful at completing the above tasks, we manually input and toggled settings to trigger errors, and found that:</p>
<table class="table table-responsive">
<thead>
<tr>
<th scope="col">Test</th>
<th scope="col">Cryptonator</th>
<th scope="col">Jaxx</th>
</tr>
</thead>
<tbody>
<tr>
<th scope="row">Address input filtering</th>
<td class="red">Does not filter for inputs not used for addresses. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_eU5WS3BfWEdXU0U" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">Does not filter for inputs not used for addresses. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_QnFrdG9RdkZsVnM" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Address input length limit</th>
<td class="red">No input length limit. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_V0JDVEhqVHA3SGM" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">No input length limit. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_THRucVliQkdSRzQ" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Amount input filtering</th>
<td class="green">Only allows numbers and a single period logically. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_OWZ1d1F3c1A1VW8" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">Filters out letters, but allows +, -, multiple periods in a row. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_WkZ4d0gwcWN1dUk" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Amount input length limit</th>
<td class="red">Does not allow the maximum length sendable in ZEC (i.e. 20999999.99999999). (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_eENteldBUS1LWXM" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="dark-red">Does not allow the maximum length sendable in ZEC (i.e. 20999999.99999999), has a bug that resets the input field when you enter in a too-small number (i.e. .00000). (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_c3dleVJkQjFwNHc" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Send to syntactically correct but invalid address</th>
<td class="green">Tells user that it is an invalid Zcash address and instructs to double check the address. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_ak5zZlotRU9RS00" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">Silently fails, no notification or UI feedback. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_eENfNUlsM1o0bWM" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Send to syntactically invalid address</th>
<td class="green">Tells user that it is an invalid Zcash address and instructs to double check the address. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_bWQ0cEJDX3Y4X1E" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">Silently fails, no notification or UI feedback. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_TFJJM1p6MnJ6dHM" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Sending payments offline</th>
<td class="green">Notifies the user that it cannot send payments offline. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_Z3ctR0dVaDB3ak0" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="dark-red">Silently fails, no notification or UI feedback. Attempt silently disappears on next start. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_TDV5aktkNktlOTg" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Sending too little (less than the fee or balance)</th>
<td class="green">Notifies the user that the amount is too little. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_N0FhZ050bzJFaXM" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="dark-red">Looks like it’s able to send, with a confirmation dialogue and everything, but it actually never goes through. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_cXBYOEdmNkZ4Zm8" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
<tr>
<th scope="row">Sending too much (more than the balance)</th>
<td class="green">Notifies the user that the amount is too much. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_bVFuM0EtT3h4TTA" target="_blank" rel="noopener noreferrer">video</a>)</td>
<td class="red">Silently fails, no notification or UI feedback. (<a href="https://drive.google.com/open?id=0B36YkvDtVNK_YlhuZlRHQVhReE0" target="_blank" rel="noopener noreferrer">video</a>)</td>
</tr>
</tbody>
</table>
<div class="subtitle"><i class="fa fa-link" aria-hidden="true"></i>
<div class="subtitle-text">
<h2 id="recommendations">Recommendations</h2>
</div>
</div>
<ol>
<li>
<p>For all crypto wallets: think about not just what the user should input or do, but all possible inputs and interactions a user can do. And if any of those are invalid, prevent users from making mistakes by filtering inputs and disabling interactions.</p>
</li>
<li>
<p>For Jaxx: users are bound to make some mistakes, so help them through it. Alert users when a transaction failed to go through, and tell them what happened (the request was canceled, we will retry sending the transaction), and give them instructions on how to fix their issue if applicable (re-check your internet connection, check the address, etc).</p>
</li>
<li>
<p>For Cryptonator: a long and task-heavy setup process will turn away most of the users before they start using your application. Get users to the wallet first, then guide then through the security steps and verify their accounts later. A good policy is to ask them to verify their device right away, ask them to verify an account hour to a day after they create their crypto wallet, and to ask if they want to enable additional security features (PINS, key backup, etc) after a set amount of use.</p>
</li>
</ol>
<p>We contacted both companies, and they have been receptive to the feedback. We look forward to making these, and other crypto wallets better in the future with further evaluation and testing.</p>
<p><!-- /wp:html --></p>