Create the 3 VPCs:

1. FinanceVPC   --> 172.31.0.0/16
2. DeveloperVPC --> 192.168.0.0/20
3. MarketingVPC --> 10.10.0.0/16 

Create EC2 instance in each VPC:
1. "FinanceServer" instance and select the "FinanceVPC"
2. "DeveloperServer" instance and select the "DeveloperVPC"
3. "MarketingServer" instance and select the "MarketingVPC"

Connecting Finance & Developer VPCs.

1. Go to "FinanceServer" and copy its private IPv4 address: 172.31.129.105
2. Go to DeveloperServer and ping the private IPv4 address of FinanceServer 172.31.129.105 --> you will receive an error because the connection is not established.

To make the connection:

3. Go to VPC, and on the left panel select "Peering Connections" and then "Create peering connection", choose a name and select the requesting VPC (DeveloperVPC) and the accepting VPCs (FinanceVPC).
4. Access request.
5. Go to the route table of each VPC and connect the other VPC i,e,. select "DeveloperVPC" --> "Route tables" --> "Edit routes" then under "Destination" add the CIDR block of "FinanceVPC", then under "Target" select the "Peering Connection" and choose the connection name you created.
6. Now go to the FinanceVPC and create the same connection, by adding the DeveloperVPC CIDR block.
7. Go to each EC2's security group and add a rule "All ICMP - IPv4" with connection to "0.0.0.0/0"

Test the connection between FinanceServer in FinanceVPC and DeveloperServer in DeveloperVPC.

1. Copy the private IPv4 address of FinanceServer and connect to the instance and ping the private address of DeveloperServer, the connection should now work.

Now create a peering connection for FinanceVPC and MarketingVPC and follow the steps to establish the connection for each server.

End of project.

