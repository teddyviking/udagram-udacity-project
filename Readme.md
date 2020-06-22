# Task
Deploying the application, along with the necessary supporting software into its matching infrastructure.

The infrastructure can be discarded as soon as the testing team finishes their tests.

# Server specs

Deploy 4 servers: 2 for each private subnet
    - two vCPUs
    - at least 4GB of RAM
    - Ubuntu 18
    - 10GB of disk space

# Security Groups and Roles

Create an IAM Role that allows your instances to use the S3 Service

Servers: 
    - inbound: HTTP Port: 80, Udagram communicates on the default, so its needed for the Load Balancer and its Health Check.
    - outbound, unrestricted internet access.

Load Balancer:
    - inbound: allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port.
    - outbound, it will only be using port 80 to reach the internal servers.

Locate servers into private subnets with a Load Balancer located in a public subnet.

Output exports of the CloudFormation script should be the public URL of the LoadBalancer.
    - Bonus points if you add http:// in front of the load balancer DNS Name in the output, for convenience.

# Other Considerations
Deploy your servers with an SSH Key into Public subnets while you are creating the script
    - Once done, move them to your private subnets and remove the SSH Key from your Launch Configuration.
    - Use a bastion instead

Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.


