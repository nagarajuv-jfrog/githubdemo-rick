---
title: post
excerpt: >-
  Returns an archive file (supports zip/tar/tar.gz/tgz) containing all the
  artifacts related to a specific build, you can optionally provide mappings to
  filter the results; the mappings support regexp capturing groups which enables
  you to dynamically construct the target path inside the result archive file.
api:
  file: artifacts-storage.json
  operationId: retrieveBuildArtifactsArchive
hidden: false
---