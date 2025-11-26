---
title: Push a Set of Artifacts to Bintray
excerpt: >-
  Push a set of artifacts to Bintray as a version. Uses a descriptor file (that
  must have `bintray-info` in its filename and a .json extension) that was
  deployed to Artifactory. The call accepts the full path to the descriptor as a
  parameter. Signing a version is controlled by the `gpgSign` parameter in the
  descriptor file and the `gpgSign` parameter passed to this command. The value
  passed to this command always takes precedence over the value in the
  descriptor file. If you also want a passphrase to be applied to your
  signature, specify `gpgPassphrase=<passphrase>`. Security: Requires a valid
  user with deploy permissions and Bintray credentials defined.
api:
  file: artifacts-storage.json
  operationId: pushArtifactsToBintray
deprecated: true
hidden: false
---