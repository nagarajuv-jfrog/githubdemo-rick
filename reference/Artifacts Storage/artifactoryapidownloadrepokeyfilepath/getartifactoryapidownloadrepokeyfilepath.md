---
title: get
excerpt: >-
  Downloads an artifact with or without returning the actual content to the
  client. When tracking the progress marks are printed (by default every 1024
  bytes). This is extremely useful if you want to trigger downloads on a remote
  Artifactory server, for example to force eager cache population of large
  artifacts, but want to avoid the bandwidth consumption involved in
  transferring the artifacts to the triggering client. If no content parameter
  is specified the file content is downloaded to the client.
api:
  file: artifacts-storage.json
  operationId: getArtifactoryApiDownloadRepokeyFilepath
hidden: false
---