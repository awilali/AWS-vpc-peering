
Overview of the project:

![vpc-peering](https://github.com/awilali/vpc-peering/assets/60300580/ff6f3062-28ed-4af5-b3fd-35827b8dad0f)

Create the 3 VPCs:

FinanceVPC --> 172.31.0.0/16 <br>
DeveloperVPC --> 192.168.0.0/20 <br>
MarketingVPC --> 10.10.0.0/16 <br>

![VPCs](https://github.com/awilali/vpc-peering/assets/60300580/083a8ecb-9c71-4c3a-ab28-707450eec56c)

Create EC2 instance in each VPC:

"FinanceServer" instance and select the "FinanceVPC" <br>
"DeveloperServer" instance and select the "DeveloperVPC" <br>
"MarketingServer" instance and select the "MarketingVPC" <br>

![servers](https://github.com/awilali/vpc-peering/assets/60300580/e2180f88-7930-41ca-8e0c-9b9e808d0ca2)

Connecting Finance & Developer VPCs.

Go to "FinanceServer" and copy its private IPv4 address: 172.31.129.105 <br>
Go to DeveloperServer and ping the private IPv4 address of FinanceServer 172.31.129.105 --> you will receive an error because the connection is not established. <br><br>
To make the connection:<br>

Go to VPC, and on the left panel select "Peering Connections" and then "Create peering connection", choose a name and select the requesting VPC (DeveloperVPC) and the accepting VPCs (FinanceVPC).
Access request.

![PeeringConnections](https://github.com/awilali/vpc-peering/assets/60300580/b77a53d8-2756-4820-84a9-00d18dcf34c8)

1. Go to the route table of each VPC and connect the other VPC i,e,. select "DeveloperVPC" --> "Route tables" --> "Edit routes" then under "Destination" add the CIDR block of "FinanceVPC", then under "Target" select the "Peering Connection" and choose the connection name you created.
2. Now go to the FinanceVPC and create the same connection, by adding the DeveloperVPC CIDR block.

FinanceVPC route table:<br>
![FinRouteTable](https://github.com/awilali/vpc-peering/assets/60300580/1ea0593e-89d5-4f21-bb8c-d6626c09eaea)

DeveloperVPC route table:<br>
![DevRouteTable](https://github.com/awilali/vpc-peering/assets/60300580/f207b432-1c0e-4cfc-b997-15275ac7af79)

3. Go to each EC2's security group and add a rule "All ICMP - IPv4" with connection to "0.0.0.0/0" <br>
4. Test the connection between FinanceServer in FinanceVPC and DeveloperServer in DeveloperVPC. <br>
5. Copy the private IPv4 address of FinanceServer and connect to the instance and ping the private address of DeveloperServer, the connection should now work. <br>

![DevFin](https://github.com/awilali/vpc-peering/assets/60300580/36424a92-db02-4fff-99c1-737c78f93e5f)

6. Now create a peering connection for FinanceVPC and MarketingVPC and follow the steps to establish the connection for each server. <br>

![FinMark](https://github.com/awilali/vpc-peering/assets/60300580/2ea793b8-1d75-444a-85bb-71a81e2fdd7a)

End of project.
