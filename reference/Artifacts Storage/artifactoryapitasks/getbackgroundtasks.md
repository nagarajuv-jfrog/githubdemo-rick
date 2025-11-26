---
title: Get Background Tasks
excerpt: >-
  Returns list of background tasks currently scheduled or running in
  Artifactory. In HA, the nodeId is added to each task. Task can be in one of
  few states: scheduled, running, stopped, cancelled. Running task also shows
  the task start time.
api:
  file: artifacts-storage.json
  operationId: getBackgroundTasks
hidden: false
---