<h1>Implement Health Checks by Using ELB and Route 53</h1>

<h2>Description</h2>
I created a target group for an Application Load Balancer, and then configured health checks for the target group. A listener routed requests from the load balancer to the target group, and then used Route 53 I configured health checks for the load balancer. Amazon Simple Notification Service (SNS) was implemented to notify me when a failure occurs, which I created a checked by simulating a web server failure.
<br/>
<br/>
The environment used contained a Virtual Private Cloud (VPC) with two public and two private subnets across two availability zones, an internet gateway, a web server in each public subnet, a security group applied to each web server, and an Application Load Balancer that has a security group applied.<br/>
<p align ="center"><img src="https://imgur.com/U8RJUyH.png" height="80%" width="80%" alt="health checks"/>
<br/>
<p>Elastic Load Balancing provides four different types of load balancers: an Application Load Balancer, a Network Load Balancer, a Classic Load Balancer, and a Gateway Load Balancer. Based on the environment and requirements, I used an Application Load Balancer because this is a web solution where monitoring is being done at Layer 7—the application layer.<br/>
<br/>
Application Load Balancers require at least one listener with at least one rule configured to perform an action. There is a default rule for which you need to configure an action. The default rule cannot be removed.</p>
<br />

<h2>Services and Resources Used</h2>

- <b>Target Groups</b>
- <b>Load Balancers</b>
- <b>Amazon Route 53</b>
- <b>Amazon CloudWatch</b>
- <b>Amazon Simple Notification Service (SNS)</b>

<h2>Project Stages:</h2>

<p align="center">
Created a target group within VPC that targeted a specific instance within an availability zone:  <br/>
<img src="https://imgur.com/vxIoJom.png" height="80%" width="80%" alt="health checks"/>
<br />
<br />
Customised the health checks for the target group:  <br/>
<img src="https://imgur.com/oC4Nbv0.png" height="80%" width="80%" alt="health checks"/>
<br />
<br />
Created an S3 bucket in AWS and uploaded the index.html file along with the profile picture for the website: <br/>
<img src="https://imgur.com/sy34MxD.png" height="80%" width="80%" alt="health checks"/>
<br />
<br />
<p align ="left">Health checks are not limited to Amazon Elastic Cloud Compute (Amazon EC2) instances. You can also create health checks for specific IP addresses and lambda functions. One of the key benefits of an Application Load Balancer is that it can perform health checks at Layer 7—the application layer.</p> <br/>
<p align="center">
Created a listener for a load balancer that forwards all traffic on port 80 to the target group and enabled group-level stickiness:  <br/>
<img src="https://imgur.com/5QRB4Hy.png" height="80%" width="80%" alt="health checks"/>
<br />
<br />
An HTTP listener uses the following actions:
<p>- Forward: Routes a request to a target group
<p>- Redirect: Redirects client requests to another URL
<p>- Fixed response: Returns a custom HTTP response or drops a client request</p>
<p align="center">
I then verified that I could connect to the web server using the DNS name of the load balancer. <br/>
<br /> 
Configured Route 53 to perform health checks for load balancer and set up CloudWatch to send Amazon SNS notifications if the health check fails: <br/>
<img src="https://imgur.com/oC4Nbv0.png" height="80%" width="80%" alt="health checks"/>
<br />
<img src="https://imgur.com/tCWsKYx.png" height="80%" width="80%" alt="health checks"/>
<br />
<br />
To simulate a server failure and checked that health check system was working, I deleted the HTTP inbound rule in the security group:  <br/>
<img src="https://imgur.com/U1ZGdMr.png" height="80%" width="80%" alt="Static Website Project Steps"/>
<br />
<br />
I then received an email notification from Route 53:  <br/>
<img src="https://imgur.com/YFzMc3v.png" height="80%" width="80%" alt="Static Website Project Steps"/>  
</p>
