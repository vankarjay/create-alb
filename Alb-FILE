{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Creating a alb",
    "Resources": {
        "myinstance": {
            "Type": "AWS::EC2::Instance",
            "Properties": {
                "ImageId": "ami-02d26659fd82cf299",
                "InstanceType": "t2.micro",
                "KeyName": "kJ",
                "Tags": [
                    {
                        "Key": "name",
                        "Value": "myinstance1"
                    }
                ],
                "SubnetId": "subnet-022a3115eda63bf2b",
                "SecurityGroupIds": [
                    {
                        "Ref": "mysg"
                    }
                ],
                "BlockDeviceMappings": [
                    {
                        "DeviceName": "/dev/xvdf",
                        "Ebs": {
                            "VolumeSize": 10,
                            "VolumeType": "gp3"
                        }
                    }
                ]
            }
        },
        "mysg": {
            "Type": "AWS::EC2::SecurityGroup",
            "Properties": {
                "GroupDescription": "Allow ssh and http",
                "SecurityGroupIngress": [
                    {
                        "CidrIp": "0.0.0.0/0",
                        "FromPort": 80,
                        "IpProtocol": "tcp",
                        "ToPort": 80
                    },
                    {
                        "CidrIp": "0.0.0.0/0",
                        "FromPort": 22,
                        "IpProtocol": "tcp",
                        "ToPort": 22
                    }
                ],
                "VpcId": "vpc-0b301e03b931e9c17"
            }
        },
        "myinstance2": {
            "Type": "AWS::EC2::Instance",
            "Properties": {
                "ImageId": "ami-0861f4e788f5069dd",
                "InstanceType": "t2.micro",
                "KeyName": "kJ",
                "Tags": [
                    {
                        "Key": "name",
                        "Value": "myinstance2"
                    }
                ],
                "SubnetId": "subnet-022a3115eda63bf2b",
                "SecurityGroupIds": [
                    {
                        "Ref": "mysg"
                    }
                ],
                "BlockDeviceMappings": [
                    {
                        "DeviceName": "/dev/xvdf",
                        "Ebs": {
                            "VolumeSize": 10,
                            "VolumeType": "gp3"
                        }
                    }
                ]
            }
        },
        "myalb": {
            "Type": "AWS::ElasticLoadBalancingV2::LoadBalancer",
            "Properties": {
                "Name": "myalb",
                "Subnets": [
                    "subnet-022a3115eda63bf2b",
                    "subnet-0a2998634a719d19b",
                    "subnet-020c7f7848d19dc88"
                ],
                "Tags": [
                    {
                        "Key": "name",
                        "Value": "myalb"
                    }
                ],
                "Type": "application",
                "SecurityGroups": [
                    {
                        "Ref": "mysg"
                    }
                ]
            }
        },
        "targetgroup": {
            "Type": "AWS::ElasticLoadBalancingV2::TargetGroup",
            "Properties": {
                "Name": "mytargetgroup",
                "Port": 80,
                "Protocol": "http",
                "Tags": [
                    {
                        "Key": "name",
                        "Value": "mytargetgroup"
                    }
                ],
                "Targets": [
                    {
                        "Id": {
                            "Ref": "myinstance"
                        },
                        "Port": 80
                    },
                    {
                        "Id": {
                            "Ref": "myinstance2"
                        },
                        "Port": 80
                    }
                ]
            }
        },
        "targetgrouplistener": {
            "Type": "AWS::ElasticLoadBalancingV2::Listener",
            "Properties": {
                "DefaultActions": [
                    {
                        "ForwardConfig": {
                            "TargetGroups": {
                                "Ref": "targetgroup"
                            }
                        }
                    }
                ],
                "LoadBalancerArn": {
                    "Ref": "myalb"
                },
                "Port": 80,
                "Protocol": "http"
            }
        }
    }
}
