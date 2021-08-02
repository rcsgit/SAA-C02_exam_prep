* How to create a key pair
    * aws ec2 create-key-pair --key-name MyKeyPair --query "KeyMaterial" --output text > MyKeyPair.pem
* Output
    * No output


* How to launch an instance
    * aws ec2 run-instances --image-id ami-a4827dc9 --count 1 --instance-type t2.micro --key-name tempKeyPair --security-group-ids sg-0741a14f2d485ad67 --subnet-id subnet-087d1f24e31ddd8af
* Output
```json
    {
        "Groups": [],
        "Instances": [
            {
                "AmiLaunchIndex": 0,
                "ImageId": "ami-",
                "InstanceId": "i-",
                "InstanceType": "t2.micro",
                "KeyName": "tempKeyPair",
                "LaunchTime": "2015-08-01"
                "Monitoring": {
                    "State": "disabled"
                },
                "Placement": {
                    "AvailabilityZone": "us-east-1a",
                    "GroupName": "",
                    "Tenancy": "default"
                },
                "PrivateDnsName": "ip-10-0-1-16.ec2.internal",
                "PrivateIpAddress": "10.0.1.16",
                "ProductCodes": [],
                "PublicDnsName": "",
                "State": {
                    "Code": 0,
                    "Name": "pending"
                },
                "StateTransitionReason": "",
                "SubnetId": "subnet-",
                "VpcId": "vpc-",
                "Architecture": "x86_64",
                "BlockDeviceMappings": [],
                "ClientToken": "----",
                "EbsOptimized": false,
                "Hypervisor": "xen",
                "NetworkInterfaces": [
                    {
                        "Attachment": {
                            "AttachTime": "2015-08-01",
                            "AttachmentId": "eni--",
                            "DeleteOnTermination": true,
                            "DeviceIndex": 0,
                            "Status": "attaching"
                        },
                        "Description": "",
                        "Groups": [
                            {
                                "GroupName": "0000001",
                                "GroupId": "sg-"
                            }
                        ],
                        "Ipv6Addresses": [],
                        "MacAddress": "02:b7::::d9",
                        "NetworkInterfaceId": "eni-",
                        "OwnerId": "---",
                        "PrivateIpAddress": "10.0.1.16",
                        "PrivateIpAddresses": [
                            {
                                "Primary": true,
                                "PrivateIpAddress": "10.0.1.16"
                            }
                        ],
                        "SourceDestCheck": true,
                        "Status": "in-use",
                        "SubnetId": "subnet-",
                        "VpcId": "vpc-",
                        "InterfaceType": "interface"
                    }
                ],
                "RootDeviceName": "/dev/xvda",
                "RootDeviceType": "ebs",
                "SecurityGroups": [
                    {
                        "GroupName": "0000001",
                        "GroupId": "sg-"
                    }
                ],
                "SourceDestCheck": true,
                "StateReason": {
                    "Code": "pending",
                    "Message": "pending"
                },
                "VirtualizationType": "hvm",
                "CpuOptions": {
                    "CoreCount": 1,
                    "ThreadsPerCore": 1
                },
                "CapacityReservationSpecification": {
                    "CapacityReservationPreference": "open"
                },
                "MetadataOptions": {
                    "State": "pending",
                    "HttpTokens": "optional",
                    "HttpPutResponseHopLimit": 1,
                    "HttpEndpoint": "enabled"
                }
            }
        ],
        "OwnerId": "----",
        "ReservationId": "r----"
    }
```

* How to check instance state
    * aws ec2 describe-instances --instance-id i-0f5a5f5e92d8aee8eaws ec2 describe-instances --instance-id i-0f5a5f5e92d8aee8e
* Output
```json
    {
    "Reservations": [
        {
            "Groups": [],
            "Instances": [
                {
                    "AmiLaunchIndex": 0,
                    "ImageId": "ami-",
                    "InstanceId": "i-",
                    "InstanceType": "t2.micro",
                    "KeyName": "tempKeyPair",
                    "LaunchTime": "2015-08-01",
                    "Monitoring": {
                        "State": "disabled"
                    },
                    "Placement": {
                        "AvailabilityZone": "us-east-1a",
                        "GroupName": "",
                        "Tenancy": "default"
                    },
                    "PrivateDnsName": "ip-10-0-1-16.ec2.internal",
                    "PrivateIpAddress": "10.0.1.16",
                    "ProductCodes": [],
                    "PublicDnsName": "",
                    "State": {
                        "Code": 16,
                        "Name": "running"
                    },
                    "StateTransitionReason": "",
                    "SubnetId": "subnet-",
                    "VpcId": "vpc-",
                    "Architecture": "x86_64",
```