,
"sgSolverWorkerInSG": {
  "Description": "Exported Security Group for Solver Worker inbound",
  "Value": { "Ref": "sgSolverWorkerInSG" },
  "Export": { "Name": { "Fn::Sub": "${AWS::StackName}-sgSolverWorkerInSG" } }
},
"sgSolverRdpInSG": {
  "Description": "Exported Security Group for Solver RDP inbound",
  "Value": { "Ref": "sgSolverRdpInSG" },
  "Export": { "Name": { "Fn::Sub": "${AWS::StackName}-sgSolverRdpInSG" } }
}
