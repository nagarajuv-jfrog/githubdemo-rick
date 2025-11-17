---
title: Connect pub Client to Artifactory
excerpt: >-
  This topic provides instructions for how to connect a supported pub client,
  like Dart or Flutter, to your pub repository in Artifactory.
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: deploy-pub-packages
      title: Deploy pub Packages
      type: basic
    - slug: copy-of-deploy-pub-packages
      title: Resolve pub Packages
      type: basic
---
You can configure your pub package management client to work with Artifactory, allowing you to natively manage pub packages in Artifactory using the CLI of your choice. Supported clients are Dart CLI and Flutter CLI.

# Prerequisites

Before connecting the Dart CLI to Artifactory, you must have an existing pub repository in Artifactory. For more information, see [Create a pub Repository](https://jfrog.com/help/r/TFrtp_Jcpcw1vmlHZ63Gmw/LaRMFN80t9Am0iMgoM88hw).

# To connect your pub package manager to Artifactory

1. Run this command to add the Artifactory repository to your client:
   ```shell Dart
   dart pub token add "https://[JFrogPlatformURL]/artifactory/api/pub/<REPO_NAME>"
   ```
   ```shell Flutter
   flutter token add "https://[JFrogPlatformURL]/artifactory/api/pub/<REPO_NAME>"
   ```
   Where:
   * `<JFrogPlatformURL>`: The URL of your JPD
   * `<REPO_NAME>`: The name of the target repository in Artifactory  
     For example:
   ```shell Dart
   dart pub token add "https://company.jfrog.io/artifactory/api/pub/pub-local"
   ```
   ```shell Flutter
   flutter pub token add "https://company.jfrog.io/artifactory/api/pub/pub-local"
   ```
2. When prompted, enter your Artifactory identity token.
3. Set the environment variable:
   ```shell
   export PUB_HOSTED_URL="https://[JFrogPlatformURL]/artifactory/api/pub/<REPO_NAME>"
   ```
   Where:
   * `<JFrogPlatformURL>`: The URL of your JPD
   * `<REPO_NAME>`: The name of the target repository in Artifactory  
     For example:
   ```shell
   export PUB_HOSTED_URL="https://company.jfrog.io/artifactory/api/pub/pub-local"
   ```

<Callout icon="✏️" theme="default">
  You can also use JFrog Set Me Up to copy the snippets populated with your token and environment. For more information, see <Anchor label="Use Artifactory Set Me Up for Configuring Package Manager Clients" target="_blank" href="https://jfrog.com/help/r/TFrtp_Jcpcw1vmlHZ63Gmw/ZQkZO1M6w04xNachSD4qrw">Use Artifactory Set Me Up for Configuring Package Manager Clients</Anchor>.
</Callout>

<br />