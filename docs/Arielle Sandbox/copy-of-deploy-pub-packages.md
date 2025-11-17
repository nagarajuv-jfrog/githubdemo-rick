---
title: Copy of Deploy pub Packages
excerpt: >-
  This topic exlpains how to use Dart CLI or Flutter CLI to deploy packages to a
  pub repository in Artifactory.
deprecated: false
hidden: false
metadata:
  robots: index
---
This procedure assumes that your package manager client is connected to Artifactory. For configuration instructions, see Connect pub Client to Artifactory.

# To deploy pub packages to Artifactory:

1. Update the version number in your `pubspec.yaml` file. 
2. Run the following command from the project root folder:    
   ```shell Dart
   dart pub publish
   ```
   ```shell Flutter
   flutter pub publish
   ```

<Callout icon="✏️">
  When manually publishing Dart and Flutter packages via the UI or REST API, they must be deployed to pub repositories according to the structure`<PACKAGE_NAME>/<PACKAGE_NAME>-<VERSION>.tar.gz`, otherwise they will not be indexed.

  The `pub publish`command automatically handles proper structure and formatting.
</Callout>

<br />