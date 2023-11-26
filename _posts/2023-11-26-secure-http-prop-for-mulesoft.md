---
layout: post
title: "Easy-Secure-Central properties management and hardening in general"
excerpt_separator: "<!--more-->"
last_modified_at: 2023-11-26T13:00:00+03:00
categories:
  - Blog
tags:
  - mulesoft
  - mule
  - properties
  - yaml
  - configuratio
  - connector
  - custom connector
---


![splash]({{ site.github.url }}/site-content/secure-http-prop/splash.png)

Among the various alternatives for securing your environment variables, a fundamental approach, without relying on a dedicated tool, is to store variables in property files. This method proves efficient and convenient during development and can be applied to production. However, as you transition to production, several additional considerations come into play:
 - who can set the variables
 - who can see the variables
 - how to manage different environment variables in relation and coordiantion with each other
 - if a variable needed to be changed in a running env, then which approach would be the fastest and errorness
 - how to seperate variable management and project artifacts management (packages should not contain properties)
 - how to integration variable management with CI/CD
 - how can this be automated
 
One approach would be, without considering vault tools due to some reasons, putting those in one central place and serving thru here. To enhance the security of these sensitive artifacts at the network level, implementing access control lists (ACLs) would be beneficial.

Using ACLs ensures that properties can only be read within their respective environments.

![alt]({{ site.github.url }}/site-content/secure-http-prop/secure-http-prop-2.png)

To safeguard the values themselves, it is essential to encrypt them to prevent unauthorized access. In certain instances, non-production passwords, especially in development environments, may be kept less complex to expedite development. However, it is evident that production passwords should not follow the same approach. 

dev.properties file
```
billing.db.url=jdbc://devdb.local
billing.db.name=billing
billing.db.user=integration_user
billing.db.pass=devPass123
```

prod.properties file
```
billing.db.url=jdbc://proddb.local
billing.db.name=billing
billing.db.user=integration_user
billing.db.pass=![encrypted-prod-passw]
```

in mulesoft version 4, this can be managed with help of below custom connector, secure-http-properties-connector.
developed connector decryptes literals which already encrypted and stored in files or http locations.

[https://github.com/farukonder/secure-http-properties-connector](https://github.com/farukonder/secure-http-properties-connector)

 - **//TODO** extend this connector to encrypt clear text based  on a given key and algorithm (mule 3 already  has a connector for encryption for clear text.)
 - **//TODO** explain how this connector can be utilized in CI/CD tools
 - **//TODO** extend this page with defining the property file update approaches

**references**
 - https://docs.mulesoft.com/mule-runtime/4.4/custom-configuration-properties-provider
 - https://www.salesforce.com/blog/custom-connector-mule-sdk/
 - https://blogs.mulesoft.com/dev-guides/api-connectors-templates/custom-connector-mule-sdk/
 - https://github.com/amitsethi0843/mule4-url-property-placeholder
 - https://docs.mulesoft.com/mule-runtime/4.2/custom-configuration-properties-provider
 - https://www.linkedin.com/pulse/mule4-loading-properties-file-from-httphttps-url-amit-sethi-1d/