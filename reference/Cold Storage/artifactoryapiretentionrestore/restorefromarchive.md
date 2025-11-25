---
title: Restore from Archive
excerpt: >-
  Triggers restoration of multiple items from the Archive. An admin can choose
  one of the following options:


  - Restore items to the original location and provide fallback repository in
  case the original location was deprecated.

  - Restore to a dedicated central repository.


  **Important:** Restore operation only moves the items back to the Warm
  instance location and does not delete them from the Cold instance.


  **Note:** This Cold Storage feature is available only for Artifactory
  Enterprise and Enterprise+ users.


  **Since:** Artifactory 7.27.3


  **Security:** Requires an admin user
api:
  file: cold-storage.json
  operationId: RestorefromArchive
hidden: false
---