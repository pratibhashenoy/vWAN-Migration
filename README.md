# Azure vWAN Migration Guide: Keeping NVA Functionality in an Updated Hub-and-Spoke Architecture

## What's This Guide For?
This high-level guide assists you in transitioning from a traditional network setup to Azure's Virtual WAN, keeping your Network Virtual Appliances (NVAs) working just as before. In scenarios where there is a traditional Hub Virtual Network with an NVA directing all traffic between On-premises and Azure and vice versa through the NVA and in cases where the requirement is that the same functionality of NVA routing must be maintained after migrating to Azure Virtual WAN i.e. The NVA will still reside in the Virtual Network and not Virtual WAN Hubs (Secure Hub).

## Why Use This Guide?
- Your preferred NVA isn't supported in Virtual WAN Hubs yet.
- You want to keep using your NVAs in Virtual Networks while enjoying Virtual WAN features.

## Current Network Architecture
You have a Classic Hub-Spoke Network:
- Two Spoke Networks. In the below diagram, it is 172.16.1.0/24 and 172.16.2.0/24.
- One Hub Network with an NVA managing traffic. In the below diagram Hub Network is 172.16.0.0/24.
- Express Route connects the on-premises networks to Azure. 
- The routing via NVA is managed using Route Tables (User Defined Routes). There is a Route Table on the Gateway Subnet in Hub Network to route traffic from On-premises to Azure Networks via NVA. Similarly, there are Route Table associated with the Spoke Network Subnet to route traffic from Azure-to-Azure Network and Azure-to-On-premises Network via NVA.

![existing-arch](/vWAN-Migration2.jpg)

## What Will Change?
You'll set up a Virtual WAN and Hub, and tweak some settings. No changes to Spoke Networks.

## How to Do It?
1. **Set Up Virtual WAN, Virtual Hub and Express Route Gateway in Virtual Hub**: Create these in Azure.
2. **Connect Express Route**: Link the Express Route circuit to the new Virtual Hub.
3. **Remove Old Connections**: Disconnect the old Express Route from the Hub Network.
4. **Delete Old Gateway**: Remove the Express Route Gateway in the Hub Network.
5. **Link Networks**: Connect the Virtual Hub to the Hub Network.
6. **Adjust Routes**: Make sure traffic from on-premises to Azure goes through the NVA. To achieve this, create a Route Table on the Virtual Hub and add the destination networks (172.16.1.0/24 and 172.16.2.0/24) to route via the new Vnet Connection. The new Vnet Connection has a Static route entry for these destination networks (172.16.1.0/24 and 172.16.2.0/24) to be routed via NVA.

![new-arch](/vWAN-Migration1.jpg)
