---
title: post
excerpt: >-
  Calculates/recalculates the Packages and Release metadata for this repository,
  based on the CRAN packages in it. The calculation can be synchronous (the
  default) or asynchronous. Supported by local repositories only. From version
  6.1, by default, the recalculation process also writes several entries from
  the CRAN package's metadata as properties on all of the artifacts (based on
  the control file's content).
api:
  file: repositories.json
  operationId: calculateCranRepositoryMetadata
hidden: false
---