# AWS Networking - Big Picture

## user interaction with app
User looks for example.com, 
**Route 53** resolves domain name to an IP address of LB located in public subnet
The traffic enters VPC through Internet Gateway.

#### Securing resources - private subnet 
To isolate resources from direct Internet, better to place them in private subnet
since Apps often require to send/receive outbound traffic, this is where NAT gateway
comes in. NAT gateway translates private IPs of EC2 to its own public IP.


1. Access via NAT gateway; instances in private subnet access S3 or Dynamo DB over Internet
through NAT gateway which cause data transfer cost and public internet connectivity.

2. VPC endpoint for private access; gateway endpoint used for S3 and Dynamo DB, directs traffic to
these services over AWS private network. Unlike NAT gateway, having no additional cost for data transfer.

Interface gateway used for other AWS services, 
it is a network interface with a private IP in your subnet powered by AWS private link.

1. A VPC peering connection is direct one to one connection between two VPCs.

2. VPN or AWS Direct Connect used to link on-prem to VPC

3. Transit gateway; simplifies connectivity which routes traffic between VPCs,
On-Prem networks and even other AWS account.

4. Setup IPSec VPN tunnel; traffic goes over Internet though.

Increase of users cause increase of cost and latency in case of using S3, ALB
Solution; ditching ALB and using cloud front; 
S3 can serve directly to users through cloudfront 
