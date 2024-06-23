Create the 3 VPCs:

1. FinanceVPC   --> 172.31.0.0/16
2. DeveloperVPC --> 192.168.0.0/20
3. MarketingVPC --> 10.10.0.0/16 

Connect the VPCs using VPC 'Peering Connections':

1. Go to "VPC", on the left panel select "Peering Connections" and then "Create peering connection", choose a name and select the requesting VPC (DeveloperVPC) and the accepting VPCs (FinanceVPC).
2. Accept the request.

3. Now create the second peering connection between the "MarketingVPC" and "FinanceVPC".
4. Accept the request.

Connect the route tables using the public subnets:

1. Go to "Route table", and select the public route table of each VPC and connect the connecting VPC i,e,. select "DeveloperVPC" --> "Route tables" --> "Edit routes" then under "Destination" add the CIDR block of "FinanceVPC", then under "Target" select the "Peering Connection" and choose the connection name you created.
2. Now go to the FinanceVPC and create the same connection, by adding the "DeveloperVPC" CIDR block inside the route table of the public subnet of "FinanceVPC".
3. Now do the same for the public subnet route table for "MarketingVPC" and "FinanceVPC"

Create EC2 instance in each VPC and select the public subnets:

1. "FinanceServer" instance and select the "FinanceVPC"
2. "DeveloperServer" instance and select the "DeveloperVPC"
3. "MarketingServer" instance and select the "MarketingVPC"

Connecting Finance & Developer VPCs.

1. Go to each EC2's security group and add a rule "All ICMP - IPv4" with connection to "0.0.0.0/0" and "SSH" - Port "20" connection to "0.0.0.0/0".

Test the connection between "FinanceServer" in FinanceVPC and DeveloperServer in "DeveloperVPC".

1. Copy the private IPv4 address of "FinanceServer" and connect to the "DeveloperVPC" instance, now ping the private address of "FinanceServer", the connection should now work.
2. Now test the connection between "FinanceServer" and "MarketingServer".

End of project.
