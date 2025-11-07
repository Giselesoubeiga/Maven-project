I updated both templates — the parent evaluation-dev.json and the evaluation-dev-securitygroups.json.
The security group file now includes the missing exports for sgSolverWorkerInSG and sgSolverRdpInSG, and the parent template references them correctly.
Let’s test it out and see if that resolves the issue.
