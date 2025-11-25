---
title: Set Logger Debug Levels
excerpt: >-
  Defines a temporary debug level for one or more loggers in memory without
  changing the logback.xml file. This request can be used to collect more
  detailed log information for a short period of time to help investigate a
  particular issue. When the defined time interval expires, the logger debug
  level is reset to its previous value.
api:
  file: loggers.json
  operationId: setLoggerDebugLevels
hidden: false
---