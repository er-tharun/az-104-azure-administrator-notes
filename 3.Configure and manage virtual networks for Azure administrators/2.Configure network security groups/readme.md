# Introduction

- Network security groups are a way to limit network traffic to resources in your virtual network. Network security groups contain a list of security rules that allow or deny inbound or outbound network traffic.
- You can assign a network security group to a subnet or a network interface, and define security rules in the group to control network traffic.

## Implement network security groups

### Things to know about network security groups

- A network security group contains a list of security rules that allow or deny inbound or outbound network traffic.

- A network security group can be associated to a subnet or a network interface.

- A network security group can be associated multiple times.

- You create a network security group and define security rules in the Azure portal.

### Network security groups and subnets

- You can assign network security groups to a subnet and create a protected screened subnet (also referred to as a demilitarized zone or DMZ). A DMZ acts as a buffer between resources within your virtual network and the internet.

- Use the network security group to restrict traffic flow to all machines that reside within the subnet.

- Each subnet can have a maximum of one associated network security group.

### Network security groups and network interfaces

- Define network security group rules to control all traffic that flows through a network interface.

- Each network interface that exists in a subnet can have zero, or one, associated network security groups.

## Determine network security group rules

### Things to know about security rules

- Azure creates several default security rules within each network security group, including inbound traffic and outbound traffic. Examples of default rules include **DenyAllInbound** traffic and **AllowInternetOutbound** traffic.
- Azure creates the default security rules in each network security group that you create.

- You can add more security rules to a network security group by specifying conditions.
- Each security rule is assigned a Priority value. All security rules for a network security group are processed in priority order. When a rule has a low Priority value, the rule has a higher priority or precedence in terms of order processing.

- You can't remove the default security rules.

- You can override a default security rule by creating another security rule that has a higher Priority setting for your network security group.

### Inbound traffic rules

- Azure defines three default inbound security rules for your network security group. These rules deny all inbound traffic except traffic from your virtual network and Azure load balancers. The next image shows the default inbound security rules for a network security group in the Azure portal.

### Outbound traffic rules

- Azure defines three default outbound security rules for your network security group. These rules only allow outbound traffic to the internet and your virtual network. The next image shows the default outbound security rules for a network security group in the Azure portal.

### Determine network security group effective rules

- Each network security group and its defined security rules are evaluated independently.
- For inbound traffic, Azure first processes network security group security rules for any associated subnets and then any associated network interfaces.
- For outbound traffic, the process is reversed. Azure first evaluates network security group security rules for any associated network interfaces followed by any associated subnets.
- For both the inbound and outbound evaluation process, Azure also checks how to apply the rules for intra-subnet traffic. Intra-subnet traffic refers to virtual machines in the same subnet.

### Network security group evaluation

- When you apply network security groups to both a subnet and a network interface, each network security group is evaluated independently. Both inbound and outbound rules are considered based on the priority and processing order.

### Things to consider when creating effective rules

- Consider allowing all traffic.
- Consider importance of allow rules.
- Consider intra-subnet traffic.
- Consider rule priority.

### View effective security rules

If you have several network security groups and aren't sure which security rules are being applied, you can use the Effective security rules link in the Azure portal. You can use the link to verify which security rules are applied to your machines, subnets, and network interfaces.

> **NOTE:** Network Watcher provides a consolidated view of your infrastructure rules.

## Implement application security groups

- You can implement application security groups (ASGs) in your Azure virtual network to logically group your virtual machines by workload. You can then define your network security group rules based on your application security groups.

### Things to know about using application security groups

- Application security groups work in the same way as network security groups, but they provide an application-centric way of looking at your infrastructure.
- You join your virtual machines to an application security group.
- Then you use the application security group as a source or destination in the network security group rules.

### Things to consider when using application security groups

- Consider IP address maintenance.
- Consider no subnets.
- Consider simplified rules.
- Consider workload support.
- Consider service tags.
- Service Tags represent a group of IP address prefixes from a specific Azure service. They help minimize the complexity of frequent updates on network security rules. While service tags are used to simplify the management of IP addresses for Azure services, ASGs are used to group VMs and manage network security policies based on those groups.
