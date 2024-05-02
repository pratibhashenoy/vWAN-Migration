# Azure vWAN Migration Guide: Keeping NVA Functionality in an Updated Hub-and-Spoke Architecture

## What's This Guide For?
This guide helps you move from a traditional network setup to Azure's Virtual WAN, keeping your Network Virtual Appliances (NVAs) working just as before. In scenarios where the traditional Hub Virtual Network has an NVA that directs all traffic between On-premises and Azure and vice-versa through the NVA and the requirement is that the same functionality of NVA routing must be maintained after migrating to Azure Virtual WAN i.e. The NVA will still reside in the Virtual Network and not Virtual WAN Hubs (Secure Hub).

## Why Use This Guide?
- Your preferred NVA isn't supported in Virtual WAN Hubs yet.
- You want to keep using your NVAs in Virtual Networks while enjoying Virtual WAN features.

## Before You Start
You have a Classic Hub-Spoke Network:
- Two Spoke Networks.
- One Hub Network with an NVA managing traffic.
- Express Route connects your on-premises setup to Azure.

![existing-arch](/vWAN-Migration2.jpg)

## What Will Change?
You'll set up a Virtual WAN and Hub, and tweak some settings. No changes to Spoke Networks.

## How to Do It?
1. **Set Up Virtual WAN and Hub**: Create these in Azure.
2. **Connect Express Route**: Link it to your new Virtual Hub.
3. **Remove Old Connections**: Disconnect the old Express Route from the Hub Network.
4. **Delete Old Gateway**: Remove the Express Route Gateway in the Hub Network.
5. **Link Networks**: Connect the Virtual Hub to the Hub Network.
6. **Adjust Routes**: Make sure traffic from on-premises to Azure goes through the NVA.

![new-arch](/vWAN-Migration1.jpg)
