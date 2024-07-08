
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
Use the exsiting jenkin job or use the below command to run from terminal (Testing)
ansible-playbook -i hosts.ini haproxy-installation.yml

# Major changes

# Security hardening
 *The HAproxy security can be increased by adding an SSL/TSL certificate for the HAproxy frontend, it encrypt traffic between the clients and HAproxy. The generated or purchased certificate can be placed under "files" directory. Sample changes in the haproxy configuration is given below.

```
frontend http
  bind :443 ssl crt /etc/haproxy/cert.pem
```

 * Rate limit
