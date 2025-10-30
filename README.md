{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "Standalone CloudFormation template to create AddressVolumeWorker EC2 instance",
  "Parameters": {
    "EnvType": {
      "Type": "String",
      "Default": "dev",
      "AllowedValues": ["dev", "cat", "prod"],
      "Description": "Environment type"
    },
    "SubnetId": {
      "Type": "AWS::EC2::Subnet::Id",
      "Description": "Subnet where the instance will be launched"
    },
    "SecurityGroupIds": {
      "Type": "List<AWS::EC2::SecurityGroup::Id>",
      "Description": "Security groups to associate with the instance"
    },
    "InstanceType": {
      "Type": "String",
      "Default": "t3.micro",
      "Description": "EC2 instance type"
    }
  },
  "Mappings": {
    "AppManagerAMI": {
      "us-east-2": { "AMI": "ami-0b13755cf8a020606" },
      "us-east-1": { "AMI": "ami-184dc970" }
    },
    "KeyConfig": {
      "us-east-2": { "Ec2KeyName": "Test" },
      "us-east-1": { "Ec2KeyName": "ACNSolverDev" }
    },
    "SolverEC2InstanceProfile": {
      "us-east-2": { "ro": "rrecs-nonprod-profile-ec2-ro" },
      "us-east-1": { "dev": "SolverDevRole" }
    }
  },
  "Resources": {
    "AddressVolumeWorker": {
      "Type": "AWS::EC2::Instance",
      "Properties": {
        "ImageId": {
          "Fn::FindInMap": [
            "AppManagerAMI",
            { "Ref": "AWS::Region" },
            "AMI"
          ]
        },
        "InstanceType": { "Ref": "InstanceType" },
        "KeyName": {
          "Fn::FindInMap": [
            "KeyConfig",
            { "Ref": "AWS::Region" },
            "Ec2KeyName"
          ]
        },
        "IamInstanceProfile": {
          "Fn::FindInMap": [
            "SolverEC2InstanceProfile",
            { "Ref": "AWS::Region" },
            "ro"
          ]
        },
        "NetworkInterfaces": [
          {
            "AssociatePublicIpAddress": false,
            "DeleteOnTermination": true,
            "DeviceIndex": 0,
            "SubnetId": { "Ref": "SubnetId" },
            "GroupSet": { "Ref": "SecurityGroupIds" }
          }
        ],
        "UserData": {
          "Fn::Base64": {
            "Fn::Join": [
              "",
              [
                "#!/bin/bash\n",
                "yum update -y\n",
                "systemctl enable amazon-ssm-agent\n",
                "systemctl start amazon-ssm-agent\n",
                "echo 'AddressVolumeWorker initialized successfully' > /var/log/init.log\n"
              ]
            ]
          }
        },
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Join": ["", [{ "Ref": "EnvType" }, "-AddressVolumeWorker"]]
            }
          },
          { "Key": "Role", "Value": "Worker" },
          { "Key": "Environment", "Value": { "Ref": "EnvType" } }
        ]
      }
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "ID of the AddressVolumeWorker EC2 instance",
      "Value": { "Ref": "AddressVolumeWorker" }
    },
    "PublicIP": {
      "Description": "Public IP of the AddressVolumeWorker (if applicable)",
      "Value": { "Fn::GetAtt": ["AddressVolumeWorker", "PublicIp"] }
    },
    "PrivateIP": {
      "Description": "Private IP of the AddressVolumeWorker",
      "Value": { "Fn::GetAtt": ["AddressVolumeWorker", "PrivateIp"] }
    }
  }
}

