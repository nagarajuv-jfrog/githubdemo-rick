---
title: Deploy Artifact by Checksum
excerpt: >-
  Deploy an artifact to the specified destination by checking if the artifact
  content already exists in Artifactory. If Artifactory already contains a
  user-readable artifact with the same checksum, the artifact content is copied
  to the new location and returns a response without requiring content transfer.
  Otherwise, a 404 error is returned to indicate that content upload is expected
  to deploy the artifact. If the X-Checksum-Deploy header is set to false, the
  artifact will be uploaded successfully with a 201 response, even if it didn't
  exist before, and submitted checksums will have the status Uploaded:
  Identical.
api:
  file: artifacts-storage-deploy.json
  operationId: DeployArtifactbyChecksum
hidden: false
---