{
    "sgSolverWorkerInSG": {
      "Type": "AWS::EC2::SecurityGroup",
      "Properties": {
        "GroupDescription": "Security group for Solver Worker inbound",
        "VpcId": { "Fn::FindInMap": ["VPCID", { "Ref": "AWS::Region" }, "VPC"] },
        "SecurityGroupIngress": [
          {
            "IpProtocol": "tcp",
            "FromPort": "8080",
            "ToPort": "8080",
            "CidrIp": "10.10.0.0/16"
          },
          {
            "IpProtocol": "tcp",
            "FromPort": "443",
            "ToPort": "443",
            "CidrIp": "10.10.0.0/16"
          }
        ],
        "SecurityGroupEgress": [
          {
            "IpProtocol": "-1",
            "CidrIp": "0.0.0.0/0"
          }
        ],
        "Tags": [
          {
            "Key": "Name",
            "Value": { "Fn::Join": ["", [{ "Ref": "EnvType" }, "-sgSolverWorkerInSG"]] }
          }
        ]
      }
    },
    "sgSolverRdpInSG": {
      "Type": "AWS::EC2::SecurityGroup",
      "Properties": {
        "GroupDescription": "Security group for RDP inbound access",
        "VpcId": { "Fn::FindInMap": ["VPCID", { "Ref": "AWS::Region" }, "VPC"] },
        "SecurityGroupIngress": [
          {
            "IpProtocol": "tcp",
            "FromPort": "3389",
            "ToPort": "3389",
            "CidrIp": "10.10.0.0/16"
          }
        ],
        "SecurityGroupEgress": [
          {
            "IpProtocol": "-1",
            "CidrIp": "0.0.0.0/0"
          }
        ],
        "Tags": [
          {
            "Key": "Name",
            "Value": { "Fn::Join": ["", [{ "Ref": "EnvType" }, "-sgSolverRdpInSG"]] }
          }
        ]
      }
    }
  }
