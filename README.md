# vpc-peering

VPC peering will allow communication between applications hosted in different VPCs by using VPC 'Peering Connections'. The Marketing and Delevoper EC2 instances need to access the Financial Services Server in the Finance Department's VPC.

![vpc-peering](https://github.com/awilali/vpc-peering/assets/60300580/11af1a72-6fdb-43f2-a84d-77663a31d8b4)

Steps to creating this solution.

The solution uses a separate VPC for each department: Marketing, Finance & Developer. The VPCs are connected by using VPC peering Connetion so that the resources in each can communicate with one another.

1. The Finance VPC is central, containing resources that are shared with the Marketing and Developer VPCs.
2. Since VPCs are isolated by default, 2 VPC peering connections are created, one connection between Marketing and Finance VPC and the other connection between the Developer and Finance VPC. A VPC peering connection is a networking connection between 2 VPCs that you can use to route traffic between them by using private IPv4 or IPv6 addresses.
3. The route tables, for each VPC, point to the revelant VPC peering connection to access the entire CIDR block of a peered VPC.
   
4. To access the Finance VPC, the public subnet 'Marketing VPC' route table points to the VPC peering connection.
5. Likewise, to access the Finance VPC, the public subnet 'Developer VPC' route table points to the VPC peering connection.
6. There's no VPC peering connection between the Marketing and Developer VPCs, thus they do not share access.
