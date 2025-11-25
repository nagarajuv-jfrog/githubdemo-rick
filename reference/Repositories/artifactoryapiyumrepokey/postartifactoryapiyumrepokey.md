---
title: post
excerpt: >-
  For Local repositories: calculates/recalculates the YUM metadata for this
  repository, based on the RPM package currently hosted in the repository.
  Supported by local, virtual, and Federated repositories. Calculation can be
  synchronous (the default) or asynchronous. For Virtual repositories,
  calculates the merged metadata from all aggregated repositories on the
  specified path. The path parameter must be passed for virtual calculation.
  Requires Artifactory Pro. Immediate calculation requests cannot be called on
  repositories with automatic asynchronous calculations enabled (applies to
  local repositories only). The path parameter applies to virtual repositories
  only. Up to version 4.8, requires a valid admin user. From version 4.8 only
  requires the set of permissions assumed by Manage (Manage + Delete/Overwrite +
  Deploy/Cache + Annotate + Read).
api:
  file: repositories.json
  operationId: postArtifactoryApiYumRepokey
hidden: false
---