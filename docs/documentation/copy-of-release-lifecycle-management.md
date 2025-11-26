---
title: Copy of Release Lifecycle Management
deprecated: false
hidden: false
metadata:
  robots: index
---
## First subhead

You need to go to the second subh[head](https://jfrog-poc-group.readme.io/jfrog-artifactorydocs/copy-of-release-lifecycle-management#yet-another-subhead)ead for that information

An essential part of delivering quality software is creating releases that are validated as they advance through the software development lifecycle (SDLC) toward their eventual consumption by end users. If not managed properly, the lifecycle of releases can become a complex process involving multiple tools and inconsistent processes used by different development teams, leading to an inefficient software supply chain.

JFrog’s Release Lifecycle Management solution centers around controlling the flow of a new version of Release Bundles (v2), which are created with the platform UI or with REST APIs from several methods, such as build outputs. The set of artifacts that define a release candidate is wrapped in the Release Bundle, which is signed with its content. The Release Bundle can then be promoted towards production via different stages known as environments (for example, DEV, INT, STG, PROD) and can also be distributed to Distribution Edge nodes.

Users with Artifactory 7.68.9 and above and JFrog Xray 3.82.6 and above can scan the contents of Release Bundles v2 and potentially block these Release Bundles from being promoted if Policy violations are identified. Users with JFrog Distribution 2.20.1 and above can also use Xray to block vulnerable Release Bundles from being distributed.

Each action performed on a Release Bundle is tracked within the JFrog Platform, including creation, promotion, and distribution, and creates signed metadata (known as evidence) attesting to that action. For more information, see ​[→Evidence Management]​​.

<Callout icon="✏️" theme="default">
  When manually publishing Dart and Flutter packages via the UI or REST API, they must be deployed to pub repositories according to the structure`<PACKAGE_NAME>/<PACKAGE_NAME>-<VERSION>.tar.gz`, otherwise they will not be indexed.
</Callout>

## Yet another subhead

<br />
