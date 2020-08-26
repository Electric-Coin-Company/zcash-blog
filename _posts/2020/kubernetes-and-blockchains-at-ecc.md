---
ID: 9944
post_title: Kubernetes and blockchains at ECC
post_name: kubernetes-and-blockchains-at-ecc
post_date: 2020-06-19 17:53:17
layout: post
link: >
  http://localhost/~ryan.zcash/electriccoinco-wordpress/blog/kubernetes-and-blockchains-at-ecc/
published: true
tags:
  - developer
categories:
  - General
  - Technical
---
<!-- wp:paragraph -->
<p>Kubernetes is an open-source project designed to manage containerized workloads. Containerization is a software development approach that allows applications to be “written once, run anywhere.” Nearly all software used today can be containerized and managed with Kubernetes. For more information on Kubernetes, including a primer of how it works, we recommend <a href="https://kubernetes.io/docs/tutorials/kubernetes-basics/" target="_blank" rel="noreferrer noopener">this guide</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This post will explain some use cases and challenges related to Kubernetes inside Electric Coin Company.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Continuous integration&nbsp;</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Let's consider the Zcash software development life cycle. Like other open-source projects using GitHub, a typical developer can commit code, collaborate with developers on proposed changes, merge in potential changes, and include these changes in tagged releases.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A pattern that works well with this software development cycle is known as "continuous integration" (CI), where proposed code changes can be validated against some definition of correctness, using programmable rules. To ensure the definition of correctness is upheld, each integration test attempt should be done from a clean and consistent starting point. This process can become tedious and repetitive, especially at scale, without container orchestration. Containers are used as a mechanism to guarantee consistency, while Kubernetes choreographs these containers to manage them on a large-scale.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>CI also provides supplemental service testing to verify the new software can still operate as expected with other programs. Likewise, Kubernetes provides the ability to run multiple versions of any supplemental service, on the same platform as the CI workloads, in a reasonable manner.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>At ECC, we currently use Buildbot as a front end for managing CI pipelines. Buildbot uses Kubernetes as a resource to actually run the work. Because Kubernetes is able to scale the available workers easily, especially during release time when project commit activity increases, Kubernetes can be configured to scale up the worker pools to handle the sudden increase in CI requests.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Kubernetes provides an excellent platform for CI work that could be used to standardize common patterns across many CI platforms. Those ideas are being formalized in new, Kubernetes-native, CI projects where Kubernetes is treated as a platform instead of a resource scheduler. At ECC we're pursuing <a href="https://tekton.dev" target="_blank" rel="noreferrer noopener">Tekton</a> as a Kubernetes-native way of performing CI. We have been running on the platform since late 2019.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Running software services</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Running software services that integrate with public decentralized blockchains reliably requires dealing with normal compute and cloud problems, as well as some unique cases.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Generally, the process involves packaging our software in Docker containers to simulate and test configuration of local and production environments. This is achieved using <code>`docker-compose`</code>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Once there is a strategy of running software locally, by itself or with some supporting services, we convert this stack into Kubernetes objects for deployment.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We have found that running software services on Kubernetes provides a number of advantages.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Scale number of instances easily</li><li>Deploy new versions, and rollback reliably</li><li>Consistent service monitoring</li><li>Lower total resource usage with limits and advanced scheduling</li><li>Built-in service discovery</li></ul>
<!-- /wp:list -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Challenges</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Most applications and software at ECC are well suited for Kubernetes. The few corner cases that exist are usually due to the decentralized nature of the projects we work on.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>State management</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Running blockchain software is all about the consensus of the shared state of all nodes on the network. Using the utxo transaction model, this means we need all transactions that have ever happened. That's a lot of state!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A new <code>`zcashd`</code> node started from scratch will take over a few hours to reach the public network consensus and be available for use as a resource on the network. When cloud-native software time startup is measured in milliseconds, this can be a big problem. Also, consider the use case of testing new software features against specific blocks or transactions. How do you fast-forward a new node to enable rapid software engineering iterations?</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The concept of a "volume" is a primitive of a containerized process, so that abstraction is well handled already. The operation challenge becomes the creation, attach/detach and cleanup of the volumes. Kubernetes can leverage a cloud provider's existing storage solutions, or you can bring your own (completely software-driven) storage solution.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The special challenge for ECC is capturing and sharing that state. For this purpose we have built a utility that will start a new node, run it to the desired block height, stop the application and gather the blockchain data. We then upload these snapshots to a cloud storage bucket or IPFS, to make available for future software runs.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Service discovery</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Kubernetes has a well-defined service discovery implementation that is quite good, but it is designed for a client/server model where clients want a single address to connect to a server, which will actually be a number of service instances.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Since the zcash network is peer-to-peer, this model doesn't map to our use case.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>But, all is not lost. We can still leverage Kuberentes service discovery features to identify peers through container labeling and then use that information to bootstrap our own discovery process per node. To learn more about our process, please reach out to us on the <a href="https://forum.zcashcommunity.com/" target="_blank" rel="noreferrer noopener">Zcash forum</a> or the Zcash <a href="https://discord.gg/KyjbTcZ" target="_blank" rel="noreferrer noopener">discord server</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:spacer {"height":20} -->
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:heading {"level":3} -->
<h3>Conclusion</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Software containerization makes development and deployment more efficient. At ECC we started with containerization, specifically using Kubernetes, to automate and orchestrate services in a way that can be shared easily throughout the organization —&nbsp;and even with people outside ECC.</p>
<!-- /wp:paragraph -->