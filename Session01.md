Walkthrough Session 01: Introduction to Azure Virtual Networks

### Introduction to Virtual Network

1. Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. VNet is similar to a traditional network that you would operate in your own data center but brings with it additional benefits of Azure's infrastructure such as scalability, availability, and isolation.

### Objectives

In this lab, you will:
1. Create a barebone solo VNet using the Azure Portal.
2. Create the same VNet using Azure Cloud CLI.
3. Use a CIDR block that will be sufficient for all future AZ-700 labs.

### Prerequisites

- An active Azure subscription.
- Basic understanding of networking concepts.

### Step 1: Create a VNet using Azure Portal

1. **Search/Create Virtual Network**.
2. Click **Create**.
3. In the **Basics** tab, enter the following details:
    - **Subscription**: Select your subscription.
    - **Resource group**: Create a new resource group or select an existing one.
    - **Name**: Enter a name for your VNet.
    - **Region**: Select the region where you want to create the VNet.
6. In the **IP Addresses** tab, enter the following details:
    - **IPv4 address space**: Enter your preferred CIDR block (e.g., `10.0.0.0/16`).
7. Leave the other settings as default and click **Review + create**.
8. Review the settings and click **Create**.

### Step 2: Create a VNet using Azure Cloud CLI

1. Open the [Azure Cloud Shell](https://shell.azure.com/).
2. Ensure you are in the Bash environment.
3. Run the following command to create a resource group:
    ```bash
    az group create --name MyResourceGroup --location eastus
    ```
4. Run the following command to create a VNet:
    ```bash
    az network vnet create \
      --name MyVNet \
      --resource-group MyResourceGroup \
      --address-prefix 10.0.0.0/16 \
      --location eastus
    ```

### Conclusion

You have successfully created a barebone solo VNet using both the Azure Portal and Azure Cloud CLI. This VNet will serve as the foundation for your future AZ-700 labs.
