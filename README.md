# Implementing Traffic Management

## Objective

In this lab, I learnt how to configure and test a public Load Balancer and an Application Gateway.

### Job Skills Learned

- Using a template to provision an infrastructure.
- Configuring an Azure Load Balancer.
- Configure an Azure Application Gateway.

### Tools Used

- Azure portal - https://portal.azure.com


## Steps

## Task 1: Use a template to provision an infrastructure
In this task, you will use a template to deploy one virtual network, one network security group, and two virtual machines.
1.	Download the \Allfiles\Lab06 lab files (template and parameters).
2.	Sign in to the Azure portal - https://portal.azure.com.
3.	Search for and select Deploy a custom template.
4.	On the custom deployment page, select Build your own template in the editor.
![image](https://github.com/user-attachments/assets/1b8a6657-43fe-49ee-9543-ee9ab712dc84)
 
5.	On the edit template page, select Load file.
6.	Locate and select the \Allfiles\Lab06\az104-06-vms-template.json file and select Open.
7.	Select Save.
8.	Select Edit parameters and load the \Allfiles\Lab06\az104-06-vms-parameters.json file.
![image](https://github.com/user-attachments/assets/1ace43c3-226a-476d-9e0c-0198192c64d7)
 
9.	Select Save.
![image](https://github.com/user-attachments/assets/2d7ac200-f8f8-4aa9-9f29-e205e90309b4)
 
10.	Use the following information to complete the fields on the custom deployment page, leaving all other fields with the default value.
![image](https://github.com/user-attachments/assets/0b6b6f1b-42a5-40f1-a163-b4c105880179)
 
11.	Select Review + Create and then select Create.


## Task 2: Configure an Azure Load Balancer
In this task, you implement an Azure Load Balancer in front of the two Azure virtual machines in the virtual network. Load Balancers in Azure provide layer 4 connectivity across resources, such as virtual machines. Load Balancer configuration includes a front-end IP address to accept connections, a backend pool, and rules that define how connections should traverse the load balancer.

*Ref 1: Architecture diagram*
![image](https://github.com/user-attachments/assets/99c940bd-727f-40b5-b1d5-0eceda956b9d)
 

1.	In the Azure portal, search for and select Load balancers and, on the Load balancers blade, click + Create.
2.	Create a load balancer with the following settings (leave others with their default values) then click Next: Frontend IP configuration:
![image](https://github.com/user-attachments/assets/db5783a0-b779-4b97-87bb-0f30e6562eae)
 
3.	On the Frontend IP configuration tab, click Add a frontend IP configuration and use the following settings:
![image](https://github.com/user-attachments/assets/5aaabf78-a77f-4088-8521-7d20730feff0)
 
4.	On the Add a public IP address popup, use the following settings before clicking OK and then Add. When completed click Next: Backend pools.
5.	On the Backend pools tab, click Add a backend pool with the following settings (leave others with their default values). Click + Add (twice) and then click Next: Inbound rules.
![image](https://github.com/user-attachments/assets/74783d62-43c5-47b3-8129-61775f93e7e8)
 
6.	As you have time, review the other tabs, then click Review + create. Ensure there are no validation errors, then click Create.
7.	Wait for the load balancer to deploy then click Go to resource.


Add a rule to determine how incoming traffic is distributed
1.	In the Settings blade, select Load balancing rules.
2.	Select + Add. Add a load balancing rule with the following settings (leave others with their default values). As you configure the rule use the informational icons to learn about each setting. When finished click Save.
![image](https://github.com/user-attachments/assets/53a53e03-fa28-4e23-a521-01e0653fde83)
 
3.	Select Frontend IP configuration from the Load Balancer page. Copy the public IP address.
4.	Open another browser tab and navigate to the IP address. Verify that the browser window displays the message Hello World from az104-06-vm0 or Hello World from az104-06-vm1.
5.	Refresh the window to verify the message changes to the other virtual machine. This demonstrates the load balancer rotating through the virtual machines.


## Task 3: Configure an Azure Application Gateway
In this task, you implement an Azure Application Gateway in front of two Azure virtual machines. An Application Gateway provides layer 7 load balancing, Web Application Firewall (WAF), SSL termination, and end-to-end encryption to the resources defined in the backend pool. The Application Gateway routes images to one virtual machine and videos to the other virtual machine.
Architecture diagram - Application Gateway
![image](https://github.com/user-attachments/assets/9c1070bc-86e3-4135-b192-c4f2f66b2e73)
 
1.	In the Azure portal, search and select Virtual networks.
2.	On the Virtual networks blade, in the list of virtual networks, click az104-06-vnet1.
3.	On the az104-06-vnet1 virtual network blade, in the Settings section, click Subnets, and then click + Subnet.
4.	Add a subnet with the following settings (leave others with their default values).
![image](https://github.com/user-attachments/assets/e296da82-8350-4738-913e-8bc332d9d1ed)
 
5.	Click Save
6.	In the Azure portal, search and select Application gateways and, on the Application Gateways blade, click + Create.
7.	On the Basics tab, specify the following settings (leave others with their default values):
![image](https://github.com/user-attachments/assets/e27b2537-f16a-495d-8555-1c2229e5f95d)
 
8.	Click Next: Frontends > and specify the following settings (leave others with their default values). When complete, click OK.
![image](https://github.com/user-attachments/assets/54fbad7a-e7ed-4b55-92d7-07d62ed1d552)
 
9.	Click Next : Backends > and then Add a backend pool. Specify the following settings (leave others with their default values). When completed click Add.
10.	Click Add a backend pool. This is the backend pool for images. Specify the following settings (leave others with their default values). When completed click Add.
11.	Click Add a backend pool. This is the backend pool for video. Specify the following settings (leave others with their default values). When completed click Add.
12.	Select Next : Configuration > and then Add a routing rule. Complete the information.
13.	Move to the Backend targets tab. Select Add after completing the basic information.
14.	In the Path-based routing section, select Add multiple targets to create a path-based rule. You will create two rules. Click Add after the first rule and then Add after the second rule.

Rule - routing to the images backend
Rule - routing to the videos backend

15.	Be sure to Save and check your changes, then select Next : Tags >. No changes are needed.
16.	Select Next : Review + create > and then click Create.
17.	After the application gateway deploys, search for and select az104-appgw.
18.	In the Application Gateway resource, in the Monitoring section, select Backend health.
19.	Ensure both servers in the backend pool display Healthy.
20.	On the Overview blade, copy the value of the Frontend public IP address.
21.	Start another browser window and test this URL - http://<frontend ip address>/image/.
22.	Verify you are directed to the image server (vm1).
23.	Start another browser window and test this URL - http://<frontend ip address>/video/.
24.	Verify you are directed to the video server (vm2).


