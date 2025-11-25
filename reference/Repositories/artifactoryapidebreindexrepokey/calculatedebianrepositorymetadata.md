---
title: post
excerpt: >-
  Calculates/recalculates the Packages and Release metadata for this repository,
  based on the Debian packages in it. Calculation can be synchronous (the
  default) or asynchronous. Supported by local repositories only. From version
  4.4, by default, the recalculation process also writes several entries from
  the Debian package's metadata as properties on all of the artifacts (based on
  the control file's content). This operation may not always be required (for
  example, if the Debian files are intact and were not modified, only the index
  needs to be recalculated. The operation is resource intensive and can be
  disabled by passing the `?writeProps=0` query param. From version 5.7, the
  target repository can be a virtual repository. Requires Artifactory Pro. Up to
  version 4.8, requires a valid admin user. From version 4.8 only requires the
  set of permissions assumed by Manage (Manage + Delete/Overwrite + Deploy/Cache
  + Annotate + Read).
api:
  file: repositories.json
  operationId: calculateDebianRepositoryMetadata
hidden: false
---