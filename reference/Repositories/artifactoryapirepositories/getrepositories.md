---
title: get
excerpt: >-
  Returns a list of minimal repository details for all repositories of the
  specified type. Filter the results using the following parameters:

  - `type` for repositories of a specific type (local, remote, virtual,
  federated, distributed)

  - `packageType` for repositories of a specific package type

  - `project` for repositories assigned to a specific project


  Note: Federated repositories are supported from Artifactory 7.18.3 and require
  an Enterprise X or Enterprise+ subscription.


  Since: 2.2.0 (packageType option was introduced in version 6.2.0)


  Security: Requires a privileged user (can be anonymous)


  Usage: `GET
  /artifactory/api/repositories[?type=(local|remote|virtual|federated|distribution)]|
  [&packageType=bower|cargo|chef|cocoapods|composer|conan|cran
  |debian|docker|gems|gitlfs|go|gradle|helm|ivy|maven|nuget|opkg|p2|pub|puppet
  |pypi|rpm|sbt|swift|terraform|vagrant|yum|generic]| [&project=projectKey]`
api:
  file: repositories.json
  operationId: getRepositories
hidden: false
---