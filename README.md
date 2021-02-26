## AWS Managed VPN

![](Connectivity-AWS-managed-VPN.svg)

| Flexibility                                | Cost                         |
| ------------------------------------------ | ---------------------------- |
| Easy setup (minutes)                       | 0.05 per VPN connection hour |
| NAT-T, AES-256, SHA-2 and latest DH groups | Data Transfer                |
| Static (1 prefix) or BGP (<100 prefixes)   |                              |
| Repeat for every VPC                       |                              |

| Resiliency                                        | Performance                      |
| ------------------------------------------------- | -------------------------------- |
| Leverage both VGW endpoints (two tunnels per VPC) | Up to 1.25 Gbps (limited at VGW) |
| Think about CGW redundancy (four tunnels per VPC) |                                  |



## Software VPN (Amazon EC2)

Allow you to use custom appliances like cicsco DMVPN or Sophos UTM suite, ... specific routing protocol or custom security feature that sits on top of the tunnel.

You can do it yourself by the obvious following steps

- Launch EC2 Instance
- Make sure to have a route to the IGW
- Make sure that the instance as an Elastic IP attached
- Install the VPN Software

or deploy a ready VPN software from AWS marketplace

![](Connectivity-Software-VPN.svg)

| Flexibility                                      | Cost                   |
| ------------------------------------------------ | ---------------------- |
| Any open source or commercial vendor             | Vendor licensing       |
| Opens up proprietary features set                | EC2 hourly cost        |
| Customer responsible for HA and scaling          | High Availability cost |
| Advanced solutions can be build using automation | Data transfer          |

| Resiliency                                                   | Performance                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| VPC endpoint HA acieved by additional EC2 instances in second AZ | Defined by EC2 instance size and type                        |
| Customer side HA is also recommended                         | Multi Gbps can be achieved per VPN instance (for all tunnels) |
|                                                              | Multiple instances for the same VPC are possible             |



## Direct Connect

**Customer presence in the DX location**

Just need to specify if need 1 or 10 Gb connection and wait for the Letter of Authorization that allows you to connect to a specific port (cross connection between customer router and AWS device)

**Customer not present in the DX location**

Circuit between customer data center and DX location through partner network provider.
In this case the Letter of Authorization has to be given to the Network provider that requires the cross connection on customer behalf.
Also in this scenario you can request a network speed that is below 1 Gbps, in this case you can get only 1 Virtual Interface

**Customer not present in the DX location**

Service provider network extending to DX location. This is relevant if you are already engaged with a service provider that already gives you connectivity with different locations and you want to extend the connectivity to AWS (ex. MPLS networks). Generally providers have their own Direct Connect accounts and they connecto to your datacenter and your VPC on top of them.

![](Connectivity-Direct-Connect.svg)

Always ask following questions to your provider to understand what is the exact scenario you are falling in:

- AWS Account that owns the DX port
- Adding / Removing Virtual Interfaces
- Routing ownership
- End-to-end costs

Resiliency

- Think about using VPN as a backup solution (it is possible to punt in place policies that favor direct connect path over VPN)
- Think about getting two different Direct Connect ports to build fault tolerance at AWS side. At the same DX location or better at 2 different DX locations
- Think about HA to the corporate side 

| Flexibility                                     | Cost                            |
| ----------------------------------------------- | ------------------------------- |
| 16 AWS regions, 67 POPs worldwide               | Port Hours                      |
| LOA available in 72 hours                       | Data out transfer               |
| Lead time of circuit build-out could take weeks | Service provider circuit / MPLS |
|                                                 | Colo cage (if applicable)       |

| Resiliency                       | Performance                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| 2 x DX in two locations + VPN    | 1 or 10 Gbps ports                                           |
| 2 x DX in two separate locations | 100, 200, 300, 400, 500 Mbps ports available through partners |
| 2 x DX in one location           | LAG several connections in a group for aggregate bandwidth   |
| DX + VPN                         | ECMP across multiples                                        |
| DX                               |                                                              |



