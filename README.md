# Introduction
Ansible role to install and configure HAproxy for Graylog clusters. The Ansible role/playbook will install the latest Haproxy as well copy the customized haproxy configuration file to the rmeote server. 


# How to deploy the Ansible Role
Use the exsiting jenkin job or use the below command to run from terminal (Testing)
```
ansible-playbook -i hosts.ini haproxy-installation.yml 
```

# Major changes
 * Implemented Rate limiting for limiting unusual traffic.

# Security hardening
 * The HAproxy security can be increased by adding an SSL/TSL certificate for the HAproxy frontend, it encrypt traffic between the clients and HAproxy. The generated or purchased certificate can be placed under "files" directory in Ansible role. Sample changes in the haproxy configuration is given below.

```
frontend http
  bind :443 ssl crt /etc/haproxy/cert.pem
```

 * Rate limiting: Rate limiting in HAProxy stops a client from making too many requests during a window of time.
```
  stick-table type ip size 100k expire 30s store http_req_rate(10s)
  http-request track-sc0 src
  http-request deny deny_status 429 if { sc_http_req_rate(0) gt 20 }
```
 * Restrict access to only trusted IP address or range, if it is not a public facing application.

```
acl trusted_network src 192.168.1.0/24
http-request deny if !trusted_network
```

## Reference
 - [HAproxy documentation](https://www.haproxy.com/blog/application-layer-ddos-attack-protection-with-haproxy)

# The Task

## Before you start

Before diving into the tasks some general remarks:

You are the owner of the code. You can use whatever library or framework you're comfortable with.

You're focusing on the usability of the tools for the development team.

## Introduction

Our cloud application is currently deployed in a single Datacenter. We currently have three environments (dev, stage, prod) to enable the development team and the quality assurance department to test the new releases.

We run our workload in a Kubernetes cluster, one for each environment. While the databases are run on classical Virtual Machines. We aggregate the logs with Graylog and ELK. The Graylog cluster is running a dedicated environment and is accessible from the intranet via a proxy.

The proxy is implemented by an HAproxy instance. To install, configure and run the HAproxy, we use an Ansible role contained in the repository. The proxy is deployed via an automated Jenkins job.

Currently, we are extending our offering, also to guarantee high availability for the application, therefore we are setting up a secondary installation of our cloud offering. In the beginning, this will be set up with an active-passive approach. We will regularly test the switchover from the primary data centre and the secondary one. To enable the developers to validate the correct switchover, we install another Graylog and ELK stack in the secondary data center.

Here, we need your help to grant access to the developers to the new Graylog cluster, via our proxy.

## Graylog proxy
1. Extend the role to serve and reach multiple Graylog clusters in different data centers. Ideally, every instance uses a different hostname.
2. What would you do to improve the reliability of the role? How could you guarantee that a new change will not break the current behavior?
3. Do you have any ideas to improve the security of the proxy?

## Notes
The connections between the intranet and the two data centers are already set up, as well as all the routing rules to reach the two data centers from the proxy.
The DNS resolution is properly configured for the proxy and the Graylog clusters.
The graylog in the primary cluster are graylog-1a, graylog-2a, graylog-3a; in the secondary graylog-1b, graylog-2, graylog-3b.

# You're done
Congratulations, this sprint was a success. Please ensure that all your code is pushed.

We'll walk through the code together in the next days.
