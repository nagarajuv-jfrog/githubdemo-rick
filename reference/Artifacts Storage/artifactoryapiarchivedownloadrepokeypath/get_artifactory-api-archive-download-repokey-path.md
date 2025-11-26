---
title: get
excerpt: >-
  Returns an archive file (supports zip/tar/tar.gz/tgz) containing all the
  artifacts that reside under the specified path (folder or repository root).
  Requires Enable Folder Download to be set. See Configuring Artifactory. From
  version 5.10, If any artifact in the folder is blocked for download by Xray,
  the whole folder download is blocked and this call will return an HTTP
  Forbidden (403) error. Requires Artifactory Pro (Multiple downloads could be
  slow and CPU Intensive). Downloading a folder or a repository's root is only
  supported for local (or cache) repositories. GET
  artifactory/api/archive/download/{repoKey}/{path}?archiveType={archiveType}[&includeChecksumFiles=true]
api:
  file: artifacts-storage.json
  operationId: get_artifactory-api-archive-download-repokey-path
hidden: false
---