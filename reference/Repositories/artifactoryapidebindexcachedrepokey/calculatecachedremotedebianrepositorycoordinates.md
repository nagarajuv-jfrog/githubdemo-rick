---
title: Calculate Cached Remote Debian Repository Coordinates
excerpt: >-
  Calculates/recalculates the Debian packages coordinates. Supported by
  remote-cache repositories only. From version 6.6.0, the coordinates
  calculation/recalculation process adds Debian packages the missing coordinates
  (Architecture, Distribution and Component) as properties, so they could be
  indexed if they would be copied/moved to a Debian local repository. Local
  repository indexing/reindexing requires those properties in order to work.
api:
  file: repositories.json
  operationId: calculateCachedRemoteDebianRepositoryCoordinates
hidden: false
---