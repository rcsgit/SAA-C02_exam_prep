* How to show VPC details
    * aws ec2 describe-vpcs --vpc-id vpc-543654683217
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
    * aws ec2 create-subnet --vpc-id vpc-654654654654 --cidr-block 10.0.1.0/24
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
            "OwnerId": "---",
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
    * aws ec2 attach-internet-gateway --vpc-id vpc-84646465654 --internet-gateway-id igw-8484736130521
* Output
    * no output

* How to create a custom route table associated with a VPC 
    * aws ec2 create-route-table --vpc-id vpc-4656546544
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
            "OwnerId": "---"
        }
    }
```

* How to create a default route
    * aws ec2 create-route --route-table-id rtb-65465578741 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-132115432151
* Output
```json 
    {
        "Return": true
    }
```

* How to check if your route has been created and is active
    * aws ec2 describe-route-tables --route-table-id rtb-4654654321561
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
    * aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-5646543213541" --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock}"
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
    * aws ec2 modify-subnet-attribute --subnet-id subnet-13213211321 --map-public-ip-on-launch
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
    * aws ec2 authorize-security-group-ingress --group-id sg-351321321 --protocol tcp --port 22 --cidr 0.0.0.0/0
* Output
    * No output

* How to add a VPC Peering
    * aws ec2 create-vpc-peering-connection --vpc-id vpc-1111 --peer-vpc-id vpc-2222
* Output
    ```json
    {
        "VpcPeeringConnection": {
            "AccepterVpcInfo": {
                "OwnerId": "---",
                "VpcId": "vpc-1111",
                "Region": "us-east-1"
            },
            "ExpirationTime": "2021-10-06T20:24:08+00:00",
            "RequesterVpcInfo": {
                "CidrBlock": "10.0.0.0/16",
                "CidrBlockSet": [
                    {
                        "CidrBlock": "10.0.0.0/16"
                    }
                ],
                "OwnerId": "---",
                "PeeringOptions": {
                    "AllowDnsResolutionFromRemoteVpc": false,
                    "AllowEgressFromLocalClassicLinkToRemoteVpc": false,
                    "AllowEgressFromLocalVpcToRemoteClassicLink": false
                },
                "VpcId": "vpc-2222",
                "Region": "us-east-1"
            },
            "Status": {
                "Code": "initiating-request",
                "Message": "Initiating Request to 78787878"
            },
            "Tags": [],
            "VpcPeeringConnectionId": "pcx-123123"
        }
    }
    ```

* How to check if a given Security Groups is being used
    * aws ec2 describe-network-interfaces --filters Name=group-id,Values=sg-3211321321 --region us-east-1 --output json
* Output
    * When there is no association:
        ```json
        {
            "NetworkInterfaces": []
        }
        ```
    * When there is association:
        ```json
            {
                "NetworkInterfaces": [
                    {
                        "Association": {
                            "IpOwnerId": "amazon",
                            "PublicDnsName": "ec2-IP.compute-1.amazonaws.com",
                            "PublicIp": "21.21.21.21"
                        },
                        "Attachment": {
                            "AttachTime": "2021-09-02T09:51:12+00:00",
                            "AttachmentId": "eni-attach-321321321",
                            "DeleteOnTermination": true,
                            "DeviceIndex": 0,
                            "InstanceId": "i-321321321",
                            "InstanceOwnerId": "---",
                            "Status": "attached"
                        },
                        "AvailabilityZone": "us-east-1b",
                        "Description": "",
                        "Groups": [
                            {
                                "GroupName": "default",
                                "GroupId": "sg-3211321321"
                            }
                        ],
                        "InterfaceType": "interface",
                        "Ipv6Addresses": [],
                        "MacAddress": "0a:34:bb:e4:b5:11",
                        "NetworkInterfaceId": "eni-32321321",
                        "OwnerId": "---",
                        "PrivateDnsName": "ip-172-31-30-212.ec2.internal",
                        "PrivateIpAddress": "172.31.30.212",
                        "PrivateIpAddresses": [
                            {
                                "Association": {
                                    "IpOwnerId": "amazon",
                                    "PublicDnsName": "ec2-IP.compute-1.amazonaws.com",
                                    "PublicIp": "21.21.21.21"
                                },
                                "Primary": true,
                                "PrivateDnsName": "ip-172-31-30-212.ec2.internal",
                                "PrivateIpAddress": "172.31.30.212"
                            }
                        ],
                        "RequesterManaged": false,
                        "SourceDestCheck": true,
                        "Status": "in-use",
                        "SubnetId": "subnet-321321321",
                        "TagSet": [],
                        "VpcId": "vpc-321321321321"
                    }
                ]
            }
        ```
