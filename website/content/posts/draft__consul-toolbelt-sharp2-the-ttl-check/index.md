---
title: "Consul Toolbelt #2: The TTL Check"
author: ""
date: 
lastmod: 2020-01-18T10:38:24-08:00
draft: true
description: ""

subtitle: "These toolbelt uses aren’t enough to warrant a full Consul install, but if you are already running Consul there are some neat things you…"

image: "/posts/draft__consul-toolbelt-sharp2-the-ttl-check/images/1.png" 
images:
 - "/posts/draft__consul-toolbelt-sharp2-the-ttl-check/images/1.png" 


aliases:
    - "/"
---

![image](/posts/draft__consul-toolbelt-sharp2-the-ttl-check/images/1.png)



These toolbelt uses aren’t enough to warrant a full Consul install, but if you are already running Consul there are some neat things you can do with it. This post is part of a series that highlights some of those uses.

Other posts in this series:

*   [Consul Toolbelt #1: Instance Health](https://medium.com/@petey5000/consul-toolbelt-1-instance-health-6415cbd4b2fe)

#### The TTL Check

Per the [Consul documentation](https://www.consul.io/docs/agent/checks.html):
> Time to Live (TTL) — These checks retain their last known state for a given TTL. The state of the check must be updated periodically over the HTTP interface. If an external system fails to update the status within a given TTL, the check is set to the failed state. This mechanism, conceptually similar to a dead man’s switch, relies on the application to directly report its health. For example, a healthy app can periodically `PUT` a status update to the HTTP endpoint; if the app fails, the TTL will expire and the health check enters a critical state. The endpoints used to update health information for a given check are the [pass endpoint](https://www.consul.io/api/agent.html#agent_check_pass) and the [fail endpoint](https://www.consul.io/api/agent.html#agent_check_fail). TTL checks also persist their last known status to disk. This allows the Consul agent to restore the last known status of the check across restarts. Persisted check status is valid through the end of the TTL from the time of the last check.

And the actual configuration looks like this:
``{  
  &#34;check&#34;: {  
    &#34;id&#34;: &#34;web-app&#34;,  
    &#34;name&#34;: &#34;Web App Status&#34;,  
    &#34;notes&#34;: &#34;Web app does a curl internally every 10 seconds&#34;,  
    &#34;ttl&#34;: &#34;30s&#34;  
  }  
}``

The pass endpoint and the fail endpoint links above don’t illustrate how or why you might use these and I don’t think it is a common use case for Consul. 

While the [Dead Man’s Switch wikipedia page](https://en.wikipedia.org/wiki/Dead_man%27s_switch) is a bit morbid, it has some good details on the nature and history of this usage. We effectively have a ticking time bomb of an alarm. If it isn’t updated at the interval we set, we’ll go into an alarm state. 

Consul supports 3 levels of alarming, Pass, Warn and Fail.

#### Use Cases

Backup scripts

Billing jobs

Canary monitors
