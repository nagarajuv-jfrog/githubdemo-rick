---
title: post
excerpt: >-
  Moves an artifact or a folder to the specified destination. Supported by local
  repositories only. Optionally suppress cross-layout module path translation
  during move. You can test the move using dry run. Move item behaves similarly
  to a standard file system and supports renames. If the target path does not
  exist, the source item is moved and optionally renamed. Otherwise, if the
  target exists and it is a directory, the source is moved and placed under the
  target directory.
api:
  file: artifacts-storage.json
  operationId: post_artifactory-api-move-srcrepokey-srcfilepath
hidden: false
---