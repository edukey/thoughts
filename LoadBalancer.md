# Dynamic Load Balancer

Dynamically add/rem node

note: Messaging are natively "dynamic" software with multi consumer on same queue (broker) : EMS, Rabbit, ...
note: historical J2EE Clusters (Weblo, Websphere, JBoss, ...) are pure software and app server dependents

- Http LB Appliance
  - F5 BigIP
  - Citrix NetScaler ADC
  - KEMP ; jetNexus ; aiScaler ADC ?
- Http LB Software
  - Win2012 NLB
  - HAProxy + Thalassa or similar config updater using sighup refresh
  - Oracle mod_weblogic apache module for Weblogic cluster
  - JBoss mod_cluster apache module for JBoss cluster

not dynamic ? Cisco ACE, Alteon, IBM WAS LoadBalancer ? 

## Elastic Load Balancer

the load balancing infra itself can resize itself
