---
title: Create Release Bundles v2
deprecated: false
hidden: false
metadata:
  robots: index
---
<Callout icon="❗️">
  **Subscription Information**

  This feature is supported on the ​Cloud (SaaS)​ platform with a ​Pro​​, ​Enterprise X​​, or ​Enterprise+​ license, and on the ​Self-Hosted​ platform with a ​Pro​​, ​Pro X​​, ​Enterprise X​ , or ​Enterprise+​​ license.
</Callout>

Creating a Release Bundle creates an immutable and signed set of content with a specified version identifier. After the Release Bundle has been created, it can be promoted to different environments with full traceability (see ​[→Promote a Release Bundle v2 Version in the Platform UI]​​).

Release Bundles v2 are created using one of the following methods:

* Platform UI
* REST API
* JFrog CLI

The platform UI supports the creation of Release Bundle v2 versions from builds and other Release Bundles. In addition to those methods, the REST API and JFrog CLI support Release Bundle v2 creation from an AQL query, a list of artifacts, and from packages.

<Callout icon="📘" theme="info">
  GPG keys must be created before you can create Release Bundles and sign them with these keys. See ​[→Create Signing Keys for Release Bundles (v2)]​​.
</Callout>
