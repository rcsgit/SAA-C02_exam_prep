# Amazon API Gateway 
# Amazon CloudFront 
# AWS Direct Connect 
# AWS Global Accelerator 
# Amazon Route 53 
# AWS Transit Gateway 
# Amazon VPC (and associated features) 

What is a VPC?

https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-subnet-basics

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
        * Subnet's CIDR is a subset of VPC's CIDR
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

We can create, access and manage VPC using any of the following interfaces:
* AWS Management Console
- AWS Command Line Interface
- AWS SDK
- Query API

Amazon VPC Quotas