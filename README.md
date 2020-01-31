# jenkins-pipelines-on-aws
Udacity Cloud DevOps NanoDegree / Jenkins Pipelines on AWS / Florian Born

# Setup the Infrastructur

## Infrastructure Diagram

### The stack
- 1 Nginx for LoadBalancing
- 2 Nginx for Serving the Website (Green/Blue)
- 1 Utility-Server (Anisble, Jenkins)
- Internet gateway
- NAT gateway

## Steps
1. Create the stack
2. Setup Webserver as Jenkins Slaves

