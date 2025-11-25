---
title: Scheduled Replication Status
excerpt: >-
  Returns the status of scheduled cron-based replication jobs defined in
  Artifactory. Supported by local, local-cached, and remote repositories. The
  status is returned on two levels, per replication job and per repository
  containing the replication jobs. Requires Artifactory Pro. Requires a user
  with 'read' permission (can be anonymous).
api:
  file: artifacts-storage-replication.json
  operationId: getScheduledReplicationStatus
hidden: false
---