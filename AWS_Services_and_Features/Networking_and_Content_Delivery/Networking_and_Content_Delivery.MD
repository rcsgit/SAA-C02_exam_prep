# Amazon API Gateway 
# Amazon CloudFront 
# AWS Direct Connect 
# AWS Global Accelerator 
# Amazon Route 53 
# AWS Transit Gateway 
# Amazon VPC (and associated features) 

What is a VPC?

Virtual Private Cloud (VPC) Is a virtual network with the benefits of using the scalable infrastructure of AWS, it is much like a private networks we would find in a data center but for your AWS account.
We can launch AWS resources into a VPC, in fact, it is the network layer for Amazon EC2.
There is no additional charge for using a VPC (there are charges for some VPC components, such as NAT gateways, Reachability Analyzer, and Traffic mirroring).

VPC concepts and components:
* VPC
    * A logically isolated virtual network dedicated to your AWS account.
    * You must specify an IPv4 address range as a CIDR block when you create your VPC, it will be primary CIDR block for your VPC
    * A VPC spans al lof the Availability Zones in the Region
    * VPC can have an optional IPv6 CIDR block
        * It is require to assign IPv6 to Subnet and EC2 instances
    * Tenancy
    * Flow Logs
* Subnet
    * A range of IP addresses in your VPC, you can launch AWS resources into a specified subnet
    * You must specify a CIDR Block when you create a Subnet
        * Subnet's CIDR block can be the same of the VPC
            * We will have a single Subnet in that VPC
        * Subnet's CIDR can be a subset of VPC's CIDR
            * We can have multiple subnets in that VPC
    * There are five reserved IP addresses in each subnet IPv4 CIDR (using a 10.0.0.0/24 CIDR block as an example):
        * 10.0.0.0
            * Network address
        * 10.0.0.1
            * Reserved by AWS for VPC router
        * 10.0.0.2
            * Reserved by AWS for Amazon DNS server
        * 10.0.0.3
            * Reserved by AWS for future use
        * 10.0.0.255
            * Network broadcast address (not supported in a VPC but reserved nevertheless)
    * Subnets are mandatory to launch resources (you must specify a subnet to launch your resources)
        * Use a public subnet for internet facing resources
            * Subnet traffic is routed to an Internet Gateway
        * Use a private subnet for internal resources
        * Use a VPN-only subnet for Site-to-Site
            * Subnet traffic is routed to a Virtual 
    * Subnets can have multiple layer of security such as Security Groups and ACLs
    * You can add one or more subnet in each Availability Zone
        * Subnet can't span Availability Zones
        * Having instances launched in different Availability zone protect your workload from the failure of a single location
    * Subnets also can be added in a Local Zone
* Route table
    * A set of rules - A.K.A routes - that are used to determine where network traffic is directed.
* Internet gateway
    * A gateway attached to your VPC to allow communication between your VPC and the Internet.
* VPC endpoint
    * Enable private connection between your VPC and supported AWS services without an Internet gateway.
* CIDR 
    * Classless Inter-Domain Routing. It is a method to allocate and routing IP addresses.
    * When you associate a CIDR block with your VPC, a route is automatically added to your VPN route tables to enable routing within the VPC

VPC and Subnet sizing For IPv4
* Primary CIDR block
    * Defined when VCP is created
    * Can't be disassociated
    * IPv4 CIDR Block between /16 (65,536 IP addresses) and /28 (16 IP Addresses)
    * It is recommended to use RFC 1918's IPv4 address range to specify primary CIDR blocks
        * 10.0.0.0 - 10.255.255.255 (10/8 prefix)
        * 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
        * 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)
* Secondary CIDR block 
    * Can be associated after VPC creation
    * Can be disassociated
    * IPv4 CIDR Block between /16 (65,536 IP addresses) and /28 (16 IP Addresses)
    * CIDR blocks must not overlap with any other existing CIDR in the same VPC
    * CIDR blocks can't be changed (increased or decreased)
    * There is a quote for CIDR blocks
    * The CIDR block must not be the same or larger than a destination CIDR ranger in a route in any of the VPC route tables
    * VPC enabled for ClassicLink can have CIDR blocks from the 10.0.0.0/16 and 10.1.0.0/16 ranges associated, but any other CIDR block from the 10.0.0.0/8 range can't be.
    * VPC peering rules (IPv4)
        * If the VPC peering connection is active
            * CIDR blocks can be added to a VPC (this block can't overlap with peer's VPN block)
        * If the VPC connection is pending-acceptance
            * The requester cannot add any CIDR block to the its VPC
                * We need to wait until the peering to be accept by the accepter before add a CIDR block, or
                * The requester can delete the peering request, it will allow a CIDR block to be added
            * The accepter can add CIDR blocks to its VPN
                * If this block overlaps with requester's VPC's CIDR block, the peering request will fail
    * When using AWS Direct Connect, the VPCs that are associated with the Direct Connect must not have overlapping CIDR blocks
    * CIDR block association states
        * associating
        * associated (ready to be used!!)
        * disassociating
        * disassociated
        * failing
        * failed
VPC and Subnet sizing For IPv6
* A single IPv6 CIDR block can be associated with a VPC or Subnet
    * IPv6 CIDR block can be disassociated from a VPC or Subnet
* We request an IPv6 block from Amazon's pool
    * VPC's CIDR block has a fixed prefix length of /56
        * Subnet's CIDR block has a prefix length of /64
    * If disassociated, we lose that IPv6 CIDR block
        * A new IPv6 CIDR block will be associated with we decide to associate a CIDR block later on
    * There are five reserved IP addresses in each subnet IPv6 CIDR (using a 2001:db8:1234:1a00/64 CIDR block as an example):
        * 2001:db8:1234:1a00::
        * 2001:db8:1234:1a00::1
        * 2001:db8:1234:1a00::2
        * 2001:db8:1234:1a00::3
        * 2001:db8:1234:1a00:ffff:ffff:ffff:ffff

Subnet routing
* Each subnet must be associated with a route table
    * All user created subnet are automatically associated with VPC's main route table
        * This association can be changed
        * VPC's main route can be changed

We can create, access and manage VPC using any of the following interfaces:
* AWS Management Console
* Command Line Interface
* AWS SDK
* Query API

Amazon VPC Quotas
* There is a quote on the number of VPCs and subnets you can create in your account
    * VPC
        * 5 per region
        * Adjustable
            * Max of 100 VPCs per region
                * increasing VPC quote will affect Internet Gateway's quote by the same amount
    * Subnet
        * 200 per VPC
        * Adjustable
    * IPv4 CIDR
        * 5
        * Adjustable
            * Max of 50 IPv4 CIDR blocks
    * IPv6 CIDR
        * 1
        * Not adjustable



References:
https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html