---
layout: post
title: "Log4m - mule4 custom json logger"
excerpt_separator: "<!--more-->"
last_modified_at: 2023-11-20T13:00:00+03:00
categories:
  - Blog
tags:
  - mulesoft
  - mule
  - logging
  - opensource
  - elasticsearch
  - json
  - connector
  - custom connector  
---


![splash]({{ site.github.url }}/site-content/log4m/log4m.min.png)

Mule comes with built-in log activity, but it has some limitations. The log4m connector, however, enhances the default features by incorporating additional capabilities.
 - Built-in JSON logger
 - Correlation ID (choose between default correlation ID or a custom one)
 - Transaction ID (business transaction ID)
 - Log type (SUCCESS or FAIL)
 - Execution point name
 - Attributes of the execution point in the flow
 - Payload:
 - - Payload
 - - Error payload (in case of flow errors)
 - - HTTP response payload (detailed information in case of HTTP errors, without requiring additional configuration)

 [https://github.com/farukonder/mule-log4m-connector](https://github.com/farukonder/mule-log4m-connector)

 *references*
  - https://blogs.mulesoft.com/dev-guides/how-to-tutorials/json-logging-mule-4/