**Walkthrough Lab Session 01** 
___
# Introduction to Azure Virtual Networks (VNets)**

1. **Azure Network** is the core of every **Azure Cloud Infrastructure**
2. Each and every **Azure Resource** reside inside an *explicit or implicit* Azure Network
3. Azure Network *product* is called **Virtual Network (VNet)**
4. The number of VNets/subnets we can create in a Resource Group/Virtual Network (VNet) in Azure depends on several factors, including the address space of the VNet/subnet and the resource limits in your subscription. 
5. By default, we can create upto 50 VNets per Azure subscription.
6. We can request an increase in VNets if needed via the Azure support portal.
7. By default, we can create up to 1,000 subnets within a single VNet in Azure.
    - This is the Azure limit for VNets in most regions.
    - This limit is subject to change, so it's always a good idea to check the      current limits via the [Azure documentation](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#virtual-network-limits).
8. Ensure you plan your address spaces and resource limits carefully.
9. A VNet is a logical container for:
- CIDR Block (IP Address Prefix)
- Subnets
- Networking configurations (DNS, Peering, Gateways, Firewalls, etc.)
10. A VNet alone does not control access; all security and routing mechanisms are applied at subnet or resource level.
11. Routing, Security, and Access Control Start at the Subnet Level. Once you divide a VNet into subnets, that’s where:
- Routing is controlled → Azure automatically provides default system routes, but you can override them with User-Defined Routes (UDRs).
- Security is enforced → Using Network Security Groups (NSGs), Azure Firewall, and Private Endpoints.
- Access control begins → Subnets define which resources can communicate, and policies are applied at the subnet level.

### Objectives
In this lab, you will:
1. Create a basic VNet and add a subnet using the Azure Shell.

### Step 1: Create a VNet using Azure Portal
1. Open the `Azure Shell`
2. Ensure you are in the Bash/Powershell environment
3. Copy and Paste the command to create Resource Group, VNet and Subnet with desired names and private IP prefixes.

```bash
# bash
# Variables for naming conventions
RESOURCE_GROUP="az700-rg-lab-eastus"
VNET_NAME="az700-vnet-lab-eastus"
ADDRESS_PREFIX="10.1.0.0/16" # VNet CIDR block (65,536 IPs)
SUBNET_NAME="az700-snet-lab-eastus"
SUBNET_PREFIX="10.1.1.0/24"  # Subnet CIDR block (256 IPs)
LOCATION="eastus"

# Create the Resource Group (if not exists)
az group create --name $RESOURCE_GROUP --location $LOCATION

# Create the VNet
az network vnet create \
  --resource-group $RESOURCE_GROUP \
  --name $VNET_NAME \
  --address-prefixes $ADDRESS_PREFIX \
  --location $LOCATION \
  --only-show-errors

# Create the Subnet
az network vnet subnet create \
  --resource-group $RESOURCE_GROUP \
  --vnet-name $VNET_NAME \
  --name $SUBNET_NAME \
  --address-prefix $SUBNET_PREFIX

# Verify the VNet and Subnet
# Display VNet with Resource Group, Name, and CIDR Prefix
echo "VNet Details:"
az network vnet show \
  --resource-group $RESOURCE_GROUP \
  --name $VNET_NAME \
  --query "{ResourceGroup:resourceGroup, VNetName:name, AddressPrefix:addressSpace.addressPrefixes}" \
  --output table

# Display all subnets with Name and CIDR Prefix
echo "Subnet Details:"
az network vnet subnet list \
  --resource-group $RESOURCE_GROUP \
  --vnet-name $VNET_NAME \
  --query "[].{SubnetName:name, AddressPrefix:addressPrefix}" \
  --output table

# Expected Output
VNet Details:
ResourceGroup              VNetName                    AddressPrefix
------------------------   ------------------------   --------------
az700-rg-lab-eastus        az700-vnet-lab-eastus      ["10.1.0.0/16"]

Subnet Details:
SubnetName                 AddressPrefix
----------------------     --------------
az700-snet-lab-eastus      10.1.1.0/24
```

### Conclusion

You have successfully created a VNet and added a Subnet to it using Azure Shell.

