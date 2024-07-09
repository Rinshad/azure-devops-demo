# Introduction
Ansible role to install and configure HAproxy.

# How to deploy the Ansible Role
Use the exsiting jenkin job or use the below command to run from terminal (Testing)
ansible-playbook -i hosts.ini haproxy-installation.yml

# Major changes
 * Implemented Rate limiting for limiting unusual traffic.

# Security hardening
 * The HAproxy security can be increased by adding an SSL/TSL certificate for the HAproxy frontend, it encrypt traffic between the clients and HAproxy. The generated or purchased certificate can be placed under "files" directory in Ansible role. Sample changes in the haproxy configuration is given below.

```
frontend http
  bind :443 ssl crt /etc/haproxy/cert.pem
```

 * Rate limiting: Rate limiting in HAProxy stops a client from making too many requests during a window of time.



# The Task

## Before you start

Before diving into the tasks some general remarks:

You are the owner of the code. You can use whatever library or framework you're comfortable with.

You're focusing on the usability of the tools for the development team.
# Azure DevOps App1 Demo with AKS, Github and ACR
 Markup : * Bullet list
              * Nested bullet
                  * Sub-nested bullet etc
          * Bullet list item 2

-OR-

 Markup : - Bullet list
              - Nested bullet
                  - Sub-nested bullet etc
          - Bullet list item 2 
* this first line

# How to deploy the Ansible Role
Use the existing jenkin job or use the below command to run from the terminal (Testing)
ansible-playbook -i hosts.ini haproxy-installation.yml

# Major changes

# Security hardening
 * The HAproxy security can be increased by adding an SSL/TSL certificate for the HAproxy frontend, it encrypts traffic between the clients and HAproxy. The generated or purchased certificate can be placed under the "files" directory. Sample changes in the HAproxy configuration are given below.

```
frontend http
  bind :443 ssl crt /etc/haproxy/cert.pem
```

 * Rate limit
