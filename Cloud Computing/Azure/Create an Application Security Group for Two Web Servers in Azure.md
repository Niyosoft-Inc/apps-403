## Create an Application Security Group for Two Web Servers in Azure

### Introduction
Your company has prepared two web servers and they intend to start serving traffic to them soon. Both servers have IIS installed, but they don't have port 80 (HTTP) or 443 (HTTPS) open for internet traffic. You have been tasked with creating an application security group, associating it with a network security group, and ensuring that the servers are accessible from the internet.

### Solution
You've been provided with Azure portal credentials and to the Windows Virtual Machines (VMs with IIS installed) with this hands-on lab.

Log in to the Azure portal using the credentials above and by clicking the `Azure Portal` button.

Create a New Application Security Group
  1. Once in the Azure portal, click on the menu in the upper-left and select Virtual Machine. Note the location of these machines, you'll need that detail momentarily.
  2. Head back to the main menu and select All Services. In the search bar type: application security groups and select that service. On the Application Security group page, click the Add button.
  3. For resource group section click the drop-down menu and select the pre-existing resource group.
  4. Under the instance details section, set the name field to asgWebServers. Ensure the region is set to the same region as your Virtual Machines (see step 1).
  5. Click review and create.

Create a New Network Security Rule
  1. Go to the Azure menu in the upper-left and select All Service and search nsg.
  2. Go to Network Security groups and click on the existing security group.
  3. Select Inbound security rules on the left, and click add.
  4. For Destination select Application Security group.
  5. For Destination application security group choose asgWebServers.
  6. The Destination port ranges are set to 80,443.
  7. Set Priority to 124.
  8. Under Name set to WebServers_Rule.
  9. Finally, click the add button. You'll see this new rule amongst your list.
  10. Head back to the Azure menu in the upper-left and select Virtual Machine.
  11. Next, we attach the application security group to the networking interface of each VM.
  12. Select your first VM.
  13. Click the Networking tab, click Application security groups.
  14. Select Configure the application security group, select aswWebServers from the drop-down, press Save.
  15. Repeat the last two steps for your second VM.


Test Connectivity to the Web Servers
  1. Click on the Overview tab on the left-hand side.
  2. Copy the Public IP address and paste it into your browser (e.g., Chrome).
  3. If successful with the previous steps, you will see the default IIS splash page.
  4. Feel free to put the other VMs IP in a browser to see its IIS splash page.

Conclusion
Congratulations — you've completed this hands-on lab!
