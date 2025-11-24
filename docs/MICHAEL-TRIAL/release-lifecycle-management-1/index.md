---
title: Release Lifecycle Management
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: get-started-with-pub
      title: Get Started with pub
      type: basic
    - title: Understanding Release Bundles v2
      type: link
      url: >-
        https://jfrog.com/help/r/jfrog-artifactory-documentation/understanding-release-bundles-v2
---
An essential part of delivering quality software is creating releases that are validated as they advance through the software development lifecycle (SDLC) toward their eventual consumption by end users. If not managed properly, the lifecycle of releases can become a complex process involving multiple tools and inconsistent processes used by different development teams, leading to an inefficient software supply chain.

JFrog’s Release Lifecycle Management solution centers around controlling the flow of a new version of Release Bundles (v2), which are created with the platform UI or with REST APIs from several methods, such as build outputs. The set of artifacts that define a release candidate is wrapped in the Release Bundle, which is signed with its content. The Release Bundle can then be promoted towards production via different stages known as environments (for example, DEV, INT, STG, PROD) and can also be distributed to Distribution Edge nodes.

Users with Artifactory 7.68.9 and above and JFrog Xray 3.82.6 and above can scan the contents of Release Bundles v2 and potentially block these Release Bundles from being promoted if Policy violations are identified. Users with JFrog Distribution 2.20.1 and above can also use Xray to block vulnerable Release Bundles from being distributed.

Each action performed on a Release Bundle is tracked within the JFrog Platform, including creation, promotion, and distribution, and creates signed metadata (known as evidence) attesting to that action. For more information, see ​[→Evidence Management]​​.

<Image border={false} src="https://files.readme.io/0eba735064e742fa1d1120811b542369268df18e7f0b443281d129c886c7fbad-image.png" />

<Callout icon="👍">
  New to RLM? The ​​JFrog Academy RLM course​​ guides you from initial setup to creating and promoting your first Release Bundle, all with complete governance, trust and auditability.
</Callout>

<Callout icon="👍">
  The JFrog CLI includes commands to facilitate the Release Lifecycle Management process. For more information, see ​CLI for JFrog Release Lifecycle Management​​.
</Callout>

## Required Subscription Levels

The following subscription levels are required for Release Lifecycle Management operations:

* ​​Create​ and ​promote​​ Release Bundles v2: Pro or above
* ​​Scan​​ Release Bundles with Xray: Pro X or above
* ​​Create​​ Xray policies that can control Release Bundle promotion: Enterprise X or above
* ​​Distribute​ Release Bundles v2 (including distribution in an ​Air Gap​​ environment): Enterprise+
* ​​Create​​ Xray policies that can control Release Bundle distribution: Enterprise+
