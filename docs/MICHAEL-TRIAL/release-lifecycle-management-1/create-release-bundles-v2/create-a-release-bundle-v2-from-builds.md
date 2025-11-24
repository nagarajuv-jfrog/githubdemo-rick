---
title: Create a Release Bundle v2 from Builds
deprecated: false
hidden: false
metadata:
  robots: index
---
Use the menu on the Release Lifecycle page to create a Release Bundle v2 from one or more builds.

<Callout icon="📘" theme="info">
  You can also create a Release Bundle v2 directly from the Builds page. For more information, see ​[→Create a Release Bundle (v2) from the Builds Table]​.
</Callout>

​​**To create a Release Bundle v2 from a build:​​**

1. In the ​**Platform**​ module, select **​Artifactory > Release Lifecycle**​​.
2. From the ​**Actions**​ menu, select ​**Create Version from Builds**​​ from the list. The New Release Bundle Version window is displayed.

<Image align="center" border={true} width="70% " src="https://files.readme.io/8c723cd35c4dc59e40d91d71d2c24fa058f3aefa831bc48aa72e49477e9ee265-image.png" className="border" />

3. In the **Release Bundle Details** tab, do the following:
   1. Enter a name for the Release Bundle. (If a Release Bundle was previously created from the selected build, its name will appear.)
   2. Enter the version number of the Release Bundle.

<Callout icon="📘" theme="info">
  Naming restrictions:

  * The name is limited to 128 characters (see Tip below).
  * The version is limited to 32 characters (see Tip below).
  * The name and version must begin with a letter, digit, or underscore.
  * The name must consist only of letters, digits, underscores, periods, and hyphens. The version support these characters and also supports the plus sign (+).
</Callout>

<Callout icon="👍">
  If a longer Release Bundle name or version is required, use the REST API or the JFrog CLI instead.
</Callout>

1. <br />
