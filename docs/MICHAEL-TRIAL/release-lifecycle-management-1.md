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
