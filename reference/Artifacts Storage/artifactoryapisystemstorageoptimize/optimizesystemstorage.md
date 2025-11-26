---
title: Optimize System Storage
excerpt: >-
  Raises a flag to invoke balancing between redundant storage units of a shared
  filestore following the next full garbage collection (from Artifactory
  Self-Hosted 4.6.0 to 7.98.x).

  Immediately triggers balancing between redundant storage units of a sharded
  filestore. If balancing is already running, the process is skipped (from
  Artifactory Self-Hosted 7.104.5 and later).


  Since: 4.6.0


  Notes: This is an advanced feature intended for administrators.


  Security: Requires a valid admin user.
api:
  file: artifacts-storage.json
  operationId: OptimizeSystemStorage
hidden: false
---