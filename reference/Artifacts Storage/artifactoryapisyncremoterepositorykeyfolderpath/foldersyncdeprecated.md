---
title: Folder Sync (Deprecated)
excerpt: >-
  Triggers a no-content download of artifacts from a remote Artifactory
  repository for all artifacts under the specified remote folder. Can optionally
  delete local files if they do not exist in the remote folder, overwrite local
  files only if they are older than remote files or never overwrite local files.
  The default is not to delete any local files and to overwrite older local
  files with remote ones. By default progress marks of the sync are displayed.
  The default timeout for the remote file list is 15000 milliseconds (15
  seconds).
api:
  file: artifacts-storage.json
  operationId: FolderSync(Deprecated)
deprecated: true
hidden: false
---