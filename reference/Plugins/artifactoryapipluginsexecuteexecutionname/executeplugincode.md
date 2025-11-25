---
title: post
excerpt: >-
  Executes a named execution closure found in the executions section of a User
  Plugins.

  Execution can take parameters and be synchronous (the default) or
  asynchronous.

  When parameters can have multiple values, you can separate the items in one of
  the following ways:

  - Use a semicolon - ; (recommended)

  - Use the encoding for the pipe ("|") character - %7C

  Alternatively, you may configure your NGINX to encode URLs so that if an
  unencoded pipe is used in the URL, NGINX will encode it to %7C. We recommend
  that you verify that this configuration does not break any other systems
  served by NGINX


  Notes: Requires Artifactory Pro

  Security: Requires an authenticated user (the plugin can control which
  users/groups are allowed to trigger it)
api:
  file: plugins.json
  operationId: executePluginCode
hidden: false
---