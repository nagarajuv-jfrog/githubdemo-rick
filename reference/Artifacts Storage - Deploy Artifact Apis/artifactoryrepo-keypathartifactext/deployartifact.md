---
title: Deploy Artifact
excerpt: >-
  Deploy an artifact to the specified destination. You can also Attach
  Properties as part of deploying artifacts. Requires a user with 'deploy'
  permissions (can be anonymous). Optionally, you can provide checksum headers
  to verify the integrity of the deployment. Artifactory rejects the deployment
  if the checksums do not match. In certain cases (particularly when working
  with large artifacts), the Created timestamp might be later than the Last
  Modified timestamp. This can occur because the Last Modified timestamp records
  when the upload began, whereas the Created timestamp is set only when the
  upload is complete and committed to the database.
api:
  file: artifacts-storage-deploy.json
  operationId: deployArtifact
hidden: false
---