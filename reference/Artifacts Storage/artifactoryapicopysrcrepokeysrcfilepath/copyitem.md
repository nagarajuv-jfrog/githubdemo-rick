---
title: Copy Item
excerpt: >-
  Copy an artifact or a folder to the specified destination. Supported for
  local, remote and Federated repositories only.


  Optionally suppress cross-layout module path translation during copy.


  You can test the copy using a dry run.


  Copy item behaves similarly to a standard file system and supports renames. If
  the target path does not exist, the source item is copied and optionally
  renamed. Otherwise, if the target exists and it is a directory,


  the source is copied and placed under the target directory.


  Notes: Requires Artifactory Pro


  Security: Requires a privileged user (can be anonymous)
api:
  file: artifacts-storage.json
  operationId: copyItem
hidden: false
---