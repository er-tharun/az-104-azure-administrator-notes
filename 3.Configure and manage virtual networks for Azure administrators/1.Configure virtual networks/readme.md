# Introduction

- Azure virtual networks are an essential component for creating private networks in Azure. They allow different Azure resources to securely communicate with each other, the internet, and on-premises networks.
- You're able to effectively use subnets, assign IP addresses, and ensure secure communication between your Azure resources and on-premises network.

# Plan virtual networks

## Things to know about Azure virtual networks

- An Azure virtual network is a logical isolation of the Azure cloud resources.
- You can use virtual networks to provision and manage virtual private networks (VPNs) in Azure.
- Each virtual network has its own Classless Inter-Domain Routing (CIDR) block and can be linked to other virtual networks and on-premises networks.
- You can link virtual networks with an on-premises IT infrastructure to create hybrid or cross-premises solutions, when the CIDR blocks of the connecting networks don't overlap.
- You control the DNS server settings for virtual networks, and segmentation of the virtual network into subnets.

## Things to consider when using virtual networks

1. **Create a dedicated private cloud-only virtual network**
   - Sometimes you don't require a cross-premises configuration for your solution. When you create a virtual network, your services and virtual machines within your virtual network can communicate directly and securely with each other in the cloud. You can still configure endpoint connections for the virtual machines and services that require internet communication, as part of your solution.
2. **Securely extend your data center with virtual networks**
   - You can build traditional site-to-site VPNs to securely scale your datacenter capacity. Site-to-site VPNs use IPSEC to provide a secure connection between your corporate VPN gateway and Azure.
3. **Enable hybrid cloud scenarios**
   - Virtual networks give you the flexibility to support a range of hybrid cloud scenarios. You can securely connect cloud-based applications to any type of on-premises system, such as mainframes and Unix systems.

# Create subnets

- Azure Subnets provide a way for you to implement logical divisions within your virtual network. Your network can be segmented into subnets to help improve security, increase performance, and make it easier to manage.

## Things to know about subnets

- Each subnet contains a range of IP addresses that fall within the virtual network address space.

- The address range for a subnet must be unique within the address space for the virtual network.

- The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.

- The IP address space for a subnet must be specified by using CIDR notation.

- You can segment a virtual network into one or more subnets in the Azure portal.

## Reserved addresses

- For each subnet, Azure reserves five IP addresses. The first four addresses and the last address are reserved.

- Let's examine the reserved addresses in an IP address range of 192.168.1.0/24

| Reserved address            | Reason                                                                |
| --------------------------- | --------------------------------------------------------------------- |
| 192.168.1.0                 | This value identifies the virtual network address.                    |
| 192.168.1.1                 | Azure configures this address as the defaultgateway.                  |
| 192.168.1.2 and 192.168.1.3 | Azure maps these Azure DNS IP addresses to the virtual network space. |
| 192.168.1.255               | This value supplies the virtual network broadcast address.            |

## Things to consider when using subnets

1. **Consider service requirements**

   - Each service directly deployed into a virtual network has specific requirements for routing and the types of traffic that must be allowed into and out of associated subnets. A service might require or create their own subnet. There must be enough unallocated space to meet the service requirements. Suppose you connect a virtual network to an on-premises network by using Azure VPN Gateway. The virtual network must have a dedicated subnet for the gateway.

2. **Consider network virtual appliances**
   - Azure routes network traffic between all subnets in a virtual network, by default. You can override Azure's default routing to prevent Azure routing between subnets. You can also override the default to route traffic between subnets through a network virtual appliance. If you require traffic between resources in the same virtual network to flow through a network virtual appliance, deploy the resources to different subnets.
3. **Consider network security groups**
   - You can associate zero or one network security group to each subnet in a virtual network. You can associate the same or a different network security group to each subnet. Each network security group contains rules that allow or deny traffic to and from sources and destinations.
4. **Consider private links**
   - Azure Private Link provides private connectivity from a virtual network to Azure platform as a service (PaaS), customer-owned, or Microsoft partner services. Private Link simplifies the network architecture and secures the connection between endpoints in Azure. The service eliminates data exposure to the public internet.

# Create virtual networks

## Things to know about creating virtual networks

- When you create a virtual network, you need to define the IP address space for the network.
- Plan to use an IP address space that's not already in use in your organization.

  - The address space for the network can be either on-premises or in the cloud, but not both.

  - Once you create the IP address space, it can't be changed. If you plan your address space for cloud-only virtual networks, you might later decide to connect an on-premises site.

- To create a virtual network, you need to define at least one subnet.

  - Each subnet contains a range of IP addresses that fall within the virtual network address space.

  - The address range for each subnet must be unique within the address space for the virtual network.

  - The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.

  ## Plan IP addressing

  - There are two types of Azure IP addresses: private and public.

    **Private IP addresses** enable communication within an Azure virtual network and your on-premises network. You create a private IP address for your resource when you use a VPN gateway or Azure ExpressRoute circuit to extend your network to Azure.

    **Public IP addresses** allow your resource to communicate with the internet. You can create a public IP address to connect with Azure public-facing services.

## Things to know about IP addresses

- IP addresses can be statically assigned or dynamically assigned.
- You can separate dynamically and statically assigned IP resources into different subnets.

- Static IP addresses don't change and are best for certain situations, such as:

  - DNS name resolution, where a change in the IP address requires updating host records.
  - IP address-based security models that require apps or services to have a static IP address.
  - TLS/SSL certificates linked to an IP address.
  - Firewall rules that allow or deny traffic by using IP address ranges.
  - Role-based virtual machines such as Domain Controllers and DNS servers.

## Things to consider when creating a public IP address

- **IP Version:** Select to create an IPv4 or IPv6 address, or Both addresses.
- **SKU:** Select the SKU for the public IP address, including Basic or Standard. The value must match the SKU of the Azure load balancer with which the address is used.
- **Name:** Enter a name to identify the IP address. The name must be unique within the resource group you select.
- **IP address assignment:** Identify the type of IP address assignment to use.
  - **Dynamic addresses** are assigned after a public IP address is associated to an Azure resource and is started for the first time. Dynamic addresses can change if a resource such as a virtual machine is stopped (deallocated) and then restarted through Azure. The address remains the same if a virtual machine is rebooted or stopped from within the guest OS. When a public IP address resource is removed from a resource, the dynamic address is released.
  - **Static addresses** are assigned when a public IP address is created. Static addresses aren't released until a public IP address resource is deleted. If the address isn't associated to a resource, you can change the assignment method after the address is created. If the address is associated to a resource, you might not be able to change the assignment method.
    > NOTE : If you select IPv6 for the IP version, the assignment method must be Dynamic for the Basic SKU. Standard SKU addresses are Static for both IPv4 and IPv6 addresses.

## Associate public IP addresses

- A public IP address resource can be associated with virtual machine network interfaces, internet-facing load balancers, VPN gateways, and application gateways. You can associate your resource with both dynamic and static public IP addresses.

## Things to consider when associating public IP addresses

| Resource            | Public IP address association | Dynamic IP address | Static IP address |
| ------------------- | ----------------------------- | ------------------ | ----------------- |
| Virtual machine     | NIC                           | Yes                | Yes               |
| Load balancer       | Front-end configuration       | Yes                | Yes               |
| VPN gateway         | VPN gateway IP configuration  | Yes                | Yes \*            |
| Application gateway | Front-end configuration       | Yes                | Yes \*            |

\* Static IP addresses are available on certain SKUs only.

## Public IP address SKUs

- When you create a public IP address, you select the Basic or Standard SKU. Your SKU choice affects the IP assignment method, security, available resources, and redundancy options.

| Feature       | Basic SKU                                                                                  | Standard SKU                                         |
| ------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| IP assignment | Static or Dynamic                                                                          | Static                                               |
| Security      | Open by default                                                                            | Secure by default, closed to inbound traffic         |
| Resources     | Network interfaces, VPN gateways, Application gateways, and internet-facing load balancers | Network interfaces or public standard load balancers |
| Redundancy    | Not zone redundant                                                                         | Zone redundant by default                            |

> **Important:** On September 30, 2025, Basic SKU public IPs will be retired.

## Allocate or assign private IP addresses

- A private IP address resource can be associated with virtual machine network interfaces, internal load balancers, and application gateways. Azure can provide an IP address (dynamic assignment) or you can assign the IP address (static assignment).

## Things to consider when associating private IP addresses

| Resource               | Private IP address association | Dynamic IP address | Static IP address |
| ---------------------- | ------------------------------ | ------------------ | ----------------- |
| Virtual machine        | NIC                            | Yes                | Yes               |
| Internal load balancer | Front-end configuration        | Yes                | Yes               |
| Application gateway    | Front-end configuration        | Yes                | Yes               |

## Private IP address assignment

- A private IP address is allocated from the address range of the virtual network subnet that a resource is deployed in. There are two options: dynamic and static.

  - **Dynamic:** Azure assigns the next available unassigned or unreserved IP address in the subnet's address range. Dynamic assignment is the default allocation method.

    - Suppose addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this case, Azure assigns the address 10.0.0.10 to a new resource.

  - **Static:** You select and assign any unassigned or unreserved IP address in the subnet's address range.

    - Suppose a subnet's address range is 10.0.0.0/16, and addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this scenario, you can assign any address between 10.0.0.10 and 10.0.255.254.
