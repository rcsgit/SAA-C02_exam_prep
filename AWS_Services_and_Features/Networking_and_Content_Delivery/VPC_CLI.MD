* How to show VPC details
    * aws ec2 describe-vpcs --vpc-id vpc-2as5d8a5d283
* output
```json
```

* How to create a VPC
    * aws ec2 create-vpc --cidr-block 10.0.0.0/16
* output:
``` json
    {
        "Vpc": {
            "CidrBlock": "10.0.0.0/16",
            "DhcpOptionsId": "dopt-",
            "State": "pending",
            "VpcId": "vpc-",
            "OwnerId": "488842980206",
            "InstanceTenancy": "default",
            "Ipv6CidrBlockAssociationSet": [],
            "CidrBlockAssociationSet": [
                {
                    "AssociationId": "vpc-cidr-",
                    "CidrBlock": "10.0.0.0/16",
                    "CidrBlockState": {
                        "State": "associated"
                    }
                }
            ],
            "IsDefault": false
        }
    }
```

* How to create a subnet associated with a VPC
    * aws ec2 create-subnet --vpc-id vpc-041fd403b804ad4cf --cidr-block 10.0.1.0/24
* Output
``` json
    {
        "Subnet": {
            "AvailabilityZone": "us-east-1f",
            "AvailabilityZoneId": "use1-az5",
            "AvailableIpAddressCount": 251,
            "CidrBlock": "10.0.1.0/24",
            "DefaultForAz": false,
            "MapPublicIpOnLaunch": false,
            "State": "available",
            "SubnetId": "subnet-",
            "VpcId": "vpc-",
            "OwnerId": "488842980206",
            "AssignIpv6AddressOnCreation": false,
            "Ipv6CidrBlockAssociationSet": [],
            "SubnetArn": "arn:aws:ec2:us-east-1::subnet/subnet-"
        }
    }
```

* How to create an Internet gateway
    * aws ec2 create-internet-gateway
* Output
``` json
    {
        "InternetGateway": {
            "Attachments": [],
            "InternetGatewayId": "igw-",
            "OwnerId": "---",
            "Tags": []
        }
    }
```

* How to attache an Internet gateway to a VPC
    * aws ec2 attach-internet-gateway --vpc-id vpc-041fd403b804ad4cf --internet-gateway-id igw-0c3f25eadfee294ae
* Output
    * no output

* How to create a custom route table associated with a VPC 
    * aws ec2 create-route-table --vpc-id vpc-041fd403b804ad4cf
* Output
``` json
    {
        "RouteTable": {
            "Associations": [],
            "PropagatingVgws": [],
            "RouteTableId": "rtb-",
            "Routes": [
                {
                    "DestinationCidrBlock": "10.0.0.0/16",
                    "GatewayId": "local",
                    "Origin": "CreateRouteTable",
                    "State": "active"
                }
            ],
            "Tags": [],
            "VpcId": "vpc-",
            "OwnerId": "488842980206"
        }
    }
```

* How to create a default route
    * aws ec2 create-route --route-table-id rtb-07a2ada181f94c00a --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0c3f25eadfee294ae
* Output
```json 
    {
        "Return": true
    }
```

* How to check if your route has been created and is active
    * aws ec2 describe-route-tables --route-table-id rtb-07a2ada181f94c00a
* Output
Look got Routes' object:
```json
    {
        "RouteTables": [
            {
                "Associations": [],
                "PropagatingVgws": [],
                "RouteTableId": "rtb-",
                "Routes": [
                    {
                        "DestinationCidrBlock": "10.0.0.0/16",
                        "GatewayId": "local",
                        "Origin": "CreateRouteTable",
                        "State": "active"
                    },
                    {
                        "DestinationCidrBlock": "0.0.0.0/0",
                        "GatewayId": "igw-",
                        "Origin": "CreateRoute",
                        "State": "active"
                    }
                ],
                "Tags": [],
                "VpcId": "vpc-",
                "OwnerId": "----"
            }
        ]
    }
```

* How to check your subnet IDs
    * aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-041fd403b804ad4cf" --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock}"
* Output
```json
    [
        {
            "ID": "subnet-",
            "CIDR": "10.0.1.0/24"
        },
        {
            "ID": "subnet-",
            "CIDR": "10.0.2.0/24"
        }
    ]
```

* How to associate a subnet to a custom route table
    * aws ec2 associate-route-table  --subnet-id subnet-00074ac8b57ce2d12 --route-table-id rtb-07a2ada181f94c00a
* Output
```json
    {
        "AssociationId": "rtbassoc-",
        "AssociationState": {
            "State": "associated"
        }
    }
```

* How to change the subnet behavior to automatically provides a public IP to EC2's instances 
    * aws ec2 modify-subnet-attribute --subnet-id subnet-00074ac8b57ce2d12 --map-public-ip-on-launch
* Output
    * No output

* How to create a security group in your VPC
    * aws ec2 create-security-group --group-name SSHAccess --description "Security group for SSH access" --vpc-id vpc-2f09a348
* Output
    ```json
    {
        "GroupId": "sg-"
    }
    ```

* How to add an ingress rule
    * aws ec2 authorize-security-group-ingress --group-id sg-0741a14f2d485ad67 --protocol tcp --port 22 --cidr 0.0.0.0/0
* Output
    * not output