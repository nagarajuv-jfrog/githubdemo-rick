---
title: Resolve pub Packages
excerpt: >-
  This topic explains how to use Dart CLI or Flutter CLI to resolvey packages
  from a pub repository in Artifactory.
deprecated: false
hidden: false
metadata:
  robots: index
---
This procedure assumes that your package manager client is connected to Artifactory. For configuration instructions, see Connect pub Client to Artifactory.

# To resolve pub packages from Artifactory:

1. Update the version number in your `pubspec.yaml` file.
2. Run the following command from the project root folder:
   ```shell Dart
   dart pub get
   ```
   ```shell Flutter
   flutter pub get
   ```

<BaluKosuri />

<br />
