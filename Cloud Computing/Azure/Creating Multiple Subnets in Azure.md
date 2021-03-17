## Creating Multiple Subnets in Azure

### Introduction
Your company wants to block communication between two VMs. They currently reside on the same network and on the same subnet. Ensure they are separated into different subnets and communication is blocked using a network security group.

### Solution
Log in to the Azure Portal using the credentials provided on the lab page.

Create a New Subnet
  1. Click the hamburger menu icon in the upper left (this is the portal menu button).
  2. Click `Virtual networks`.
  3. Click the provided virtual network.
  4. Click `Subnets` in the left-hand menu.
  5. Click `+ Subnet`.
  6. In the pane that appears, set the following values:
        - Name: subnet2
        - Address range (CIDR block): 10.0.1.0/24
  7. Click `OK`.
  

Create New Network Security Group Rules
  1. Click the portal menu button in the upper left.
  2. Click `All services`.
  3. Search for "nsg".
  4. In the search results, click `Network security groups`.
  5. Click the provided network security group.
  6. Click `Inbound security rules` in the left-hand menu.
  7. Click `+ Add`.
  8. In the pane that appears, set the following values:
        - Source: IP Addresses
        - Source IP addresses/CIDR ranges: 10.0.1.0/24
        - Source port ranges: *
        - Destination: Any
        - Destination port ranges: *
        - Protocol: Any
        - Action: Deny
        - Priority: 100
        - Name: block_all_subnet2
  9. Click `Add`.
  10. Click `Outbound security rules` in the left-hand menu.
  11. Click `+ Add`.
  12. In the pane that appears, set the following values:
        - Source: IP Addresses
        - Source IP addresses/CIDR ranges: 10.0.0.0/24
        - Source port ranges: *
        - Destination: IP Addresses
        - Destination IP addresses: 10.0.1.0/24
        - Destination port ranges: *
        - Protocol: Any
        - Action: Deny
        - Priority: 100
        - Name: block_all_subnet2_out
  13. Click `Add`.
  

Move the VM to the New Subnet
  1. Click the portal menu button in the upper left.
  2. Click `Virtual machines`.
  3. Click `linVM`.
  4. Click `Networking` in the left-hand menu.
  5. Click the listed network interface (it'll be named something like `nic2-bhfpm`).
  6. Click `IP configurations` in the left-hand menu.
  7. In the `Subnet` dropdown, click to select `subnet2`.
  8. Click `Save`.
  9. Click `Virtual machines` in the breadcrumb link trail at the top of the screen.
  10. Click `winVM`.
  11. Click  `Connect > RDP`.
  12. Click `Download RDP File`.
  13. Open the RDP file, and log in to the VM using the credentials provided on the lab page.
  14. In the Windows VM, click the Windows menu button in the lower left and search for "CMD".
  15. Select the Command Prompt desktop app.
  16. Attempt to ping `subnet2`:

`ping 10.0.1.4`

We'll see a message saying `Request timed out`. This means the communication is blocked, so we were successful in our lab objectives.

Conclusion
Congratulations — you've completed this hands-on lab!
