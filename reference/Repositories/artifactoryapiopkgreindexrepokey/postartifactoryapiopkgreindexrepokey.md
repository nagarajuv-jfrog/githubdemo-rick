---
title: post
excerpt: >-
  Calculates/recalculates the Packages and Release metadata for this repository,
  based on the ipk packages in it (in each feed location). Calculation can be
  synchronous (the default) or asynchronous. Supported by local repositories
  only. By default, the recalculation process also writes several entries from
  the ipk package's metadata as properties on all of the artifacts (based on the
  control file's content). This operation may not always be required (for
  example, if the ipk files are intact and were not modified, only the index
  needs to be recalculated. The operation is resource intensive and can be
  disabled by passing the `?writeProps=0` query param.
api:
  file: repositories.json
  operationId: postArtifactoryApiOpkgReindexRepokey
hidden: false
---