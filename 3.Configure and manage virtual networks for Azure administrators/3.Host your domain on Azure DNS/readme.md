# Introduction

- Azure DNS lets you host your Domain Name System (DNS) records for your domains on Azure infrastructure.

### What is Azure DNS?

- Azure DNS is a hosting service for Domain Name System (DNS) domains that provides name resolution by using Microsoft Azure infrastructure.

### What is DNS?

- DNS, or the Domain Name System, is a protocol within the TCP/IP standard. DNS serves an essential role of translating the human-readable domain names—for example: www.wideworldimports.com—into a known IP address. IP addresses enable computers and network devices to identify and route requests among themselves.
- DNS uses a global directory hosted on servers around the world. Microsoft is part of the network that provides a DNS service through Azure DNS.

- A DNS server is also known as a DNS name server, or just a name server.

### How does DNS work?

A DNS server carries out one of two primary functions:

- Maintains a local cache of recently accessed or used domain names and their IP addresses. This cache provides a faster response to a local domain lookup request. If the DNS server can't find the requested domain, it passes the request to another DNS server. This process repeats at each DNS server until either a match is made or the search times out.
- Maintains the key-value pair database of IP addresses and any host or subdomain over which the DNS server has authority. This function is often associated with mail, web, and other internet domain services.

### Domain lookup requests

- If the domain name is stored in the short-term cache, the DNS server resolves the domain request.
- If the domain isn't in the cache, it contacts one or more DNS servers on the web to see if they have a match. When a match is found, the DNS server updates the local cache and resolves the request.
- If the domain isn't found after a reasonable number of DNS checks, the DNS server responds with a domain cannot be found error.

### IPv4 and IPv6

- **IPv4** is composed of four sets of numbers, in the range 0 to 255, each separated by a dot; for example: 127.0.0.1. Today, IPv4 is the most commonly used standard. Yet, with the increase in IoT devices, the IPv4 standard will eventually be unable to keep up.

- **IPv6** is a relatively new standard and is intended to eventually replace IPv4. It consists of eight groups of hexadecimal numbers, each separated by a colon; for example: fe80:11a1:ac15:e9gf:e884:edb0:ddee:fea3.
- Many network devices are now provisioned with both an IPv4 and an IPv6 address. The DNS name server can resolve domain names to both IPv4 and IPv6 addresses.

### DNS settings for your domain

- Whether a third-party host your DNS server or you manage it in-house, you need to configure it for each host type you're using. Host types include web, email, or other services you're using.

- As the administrator for your company, you want to set up a DNS server by using Azure DNS. In this instance, the DNS server acts as a start of authority (SOA) for your domain.

### DNS record types

Configuration information for your DNS server is stored as a file within a zone on your DNS server. Each file is called a record.

- **A** is the host record, and is the most common type of DNS record. It maps the domain or host name to the IP address.
- **CNAME** is a Canonical Name record that's used to create an alias from one domain name to another domain name. If you had different domain names that all accessed the same website, you'd use CNAME.
- **MX** is the mail exchange record. It maps mail requests to your mail server, whether hosted on-premises or in the cloud.
- **TXT** is the text record. It's used to associate text strings with a domain name. Azure and Microsoft 365 use TXT records to verify domain ownership.

Additionally, there are the following record types:

- Wildcards
- CAA (certificate authority)
- NS (name server)
- SOA (start of authority)
- SPF (sender policy framework)
- SRV (server locations)

---

> The SOA and NS records are created automatically when you create a DNS zone by using Azure DNS.

### Record sets

- Some record types support the concept of record sets, or resource record sets. A record set allows for multiple resources to be defined in a single record. For example, here's an A record that has one domain with two IP addresses:
  <br />
  www.wideworldimports.com. 3600 IN A 127.0.0.1
  <br />
  www.wideworldimports.com. 3600 IN A 127.0.0.2

### What is Azure DNS?

- Azure DNS allows you to host and manage your domains by using a globally distributed name-server infrastructure. It allows you to manage all of your domains by using your existing Azure credentials.

- Azure DNS acts as the SOA for the domain.

- You can't use Azure DNS to register a domain name; you need to register it by using a third-party domain registrar.

### Why use Azure DNS to host your domain?

Azure DNS is built on the Azure Resource Manager service, which offers the following benefits:

- Improved security
- Ease of use
- Private DNS domains
- Alias record sets
  > **NOTE:** At this time, Azure DNS doesn't support **Domain Name System Security Extensions.** If you require this security extension, you should host those portions of your domain with a third-party provider.

### Security features

- **Role-based access control**, which gives you fine-grained control over users' access to Azure resources. You can monitor their usage and control the resources and services to which they have access.
- **Activity logs**, which let you track changes to a resource and pinpoint where faults occurred.
- **Resource locking**, which gives you a greater level of control to restrict or remove access to resource groups, subscriptions, or any Azure resources.

### Private domains

- Azure DNS handles translating external domain names to IP addresses. Azure DNS lets you create private zones. These zones provide name resolution for virtual machines (VMs) within a virtual network and between virtual networks without having to create a custom DNS solution. Private zones allow you to use your own custom domain names rather than the Azure-provided names.
- To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.

Private DNS zones have the following benefits:

- DNS zones are supported as part of the Azure infrastructure, so there's no need to invest in a DNS solution.
- All DNS record types are supported: A, CNAME, TXT, MX, SOA, AAAA, PTR, and SRV.
- Host names for VMs in your virtual network are automatically maintained.
- **Split-horizon DNS support** allows the same domain name to exist in both private and public zones. It resolves to the correct one based on the originating request location.

### Alias record sets

- Alias records sets can point to an Azure resource. For example, you can set up an alias record to direct traffic to an Azure public IP address, an Azure Traffic Manager profile, or an Azure Content Delivery Network endpoint.

The alias record set is supported in the following DNS record types:

- A
- AAAA
- CNAME

---

## Configure a public DNS zone

- Create a DNS zone in Azure.
- Get your Azure DNS name servers.
- Update the domain registrar setting.
- Verify delegation of domain name services
- Configure your custom DNS settings

> **NOTE:** Changing the NS details is called `domain delegation`. When you delegate the domain, you must use all four name servers provided by Azure DNS.
> <br />
> To verify the success of the domain delegation, query the start of authority (SOA) record. The SOA record is automatically created when the Azure DNS zone is set up. You can verify the SOA record using a tool like nslookup.

The SOA record represents your domain and becomes the reference point when other DNS servers are searching for your domain on the internet.

```cmd
nslookup -type=SOA wideworldimports.com
```

### A record

Each A record requires the following details:

- Name: The name of the custom domain, for example webserver1.
- Type: In this instance, it's A.
- TTL: Represents the "time-to-live" as a whole unit, where 1 is one second. This value indicates how long the A record lives in a DNS cache before it expires.
- IP address: The IP address of the server to which this A record should resolve.

### CNAME record

The CNAME is the canonical name, or the alias for an A record. Use CNAME when you have different domain names that all access the same website. For example, you might need a CNAME in the wideworldimports zone if you want both www.wideworldimports.com and wideworldimports.com to resolve to the same IP address.

You'd create the CNAME record in the wideworldimports zone with the following information:

- NAME: www
- TTL: 600 seconds
- Record type: CNAME

If you exposed a web function, you'd create a CNAME record that resolves to the Azure function.

### Configure a private DNS zone

Another type of DNS zone that you can configure and host in Azure is a private DNS zone. Private DNS zones aren't visible on the Internet, and don't require that you use a domain registrar. You can use private DNS zones to assign DNS names to virtual machines (VMs) in your Azure virtual networks.

- Create a private DNS zone.
- Identify virtual networks.
- Link your virtual network to a private DNS zone.

## Dynamically resolve resource name by using alias record

### What is an apex domain?

- The apex domain is your domain's highest level. In our case, that's wideworldimports.com. The apex domain is also sometimes referred to as the zone apex or root apex. The @ symbol often represents the apex domain in your DNS zone records.
- If you check the DNS zone for wideworldimports.com, you see that there are two apex domain records: NS and SOA. The NS and SOA records are automatically created when you created the DNS zone.
- CNAME records that you might need for an Azure Traffic Manager profile or Azure Content Delivery Network endpoints aren't supported at the zone apex level. However, other alias records are supported at the zone apex level.

### What are alias records?

Azure alias records enable a zone apex domain to reference other Azure resources from the DNS zone. You don't need to create complex redirection policies. You can also use an Azure alias to route all traffic through Traffic Manager.

The Azure alias record can point to the following Azure resources:

- A Traffic Manager profile
- Azure Content Delivery Network endpoints
- A public IP resource
- A front-door profile

Alias records provide lifecycle tracking of target resources, ensuring that changes to any target resource are automatically applied to the DNS zone. Alias records also provide support for load-balanced applications in the zone apex.

The alias record set supports the following DNS zone record types:

- A: The IPv4 domain name-mapping record.
- AAAA: The IPv6 domain name-mapping record.
- CNAME: The alias for your domain, which links to the A record.

### Uses for alias records

- Prevents dangling DNS records
- Updates DNS record set automatically when IP addresses change.
- Hosts load-balanced applications at the zone apex.
- Points zone apex to Azure Content Delivery Network endpoints.

An alias record allows you to link the zone apex (wideworldimports.com) to a load balancer. It creates a link to the Azure resource rather than a direct IP-based connection. So, if the IP address of your load balancer changes, the zone apex record continues to work.
