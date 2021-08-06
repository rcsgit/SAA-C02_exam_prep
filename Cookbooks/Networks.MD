
* Listing VPCs
    * Listing all VPCs
        * aws ec2 describe-vpcs
    * Listing a single VPC
        * aws ec2 describe-vpcs --vpc-ids vpc-111111
    * Listing a list of VPCs
        * aws ec2 describe-vpcs --vpc-ids vpc-111111 vpc-222222

* Creates a VPC with a default CIDR block
    * aws ec2 create-vpc --cidr-block 10.0.0.0/16 