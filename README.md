I’ve completed the first worker Auto Scaling Group template (addressvolumefactor) for the commercial environment.

The file is named Gisele-Worker-ASG-AddressVolumeFactor.yaml, and it includes:

Region: us-east-2

Account: 633665788591

Launch config: RRECS-Solver-Test-Worker-T3Medium-java21-github-Spot

Mappings and subnet values pulled from evaluation-dev.json

ASG only (no launch config)

Can you please take a look and let me know if it aligns with what you and Pratik had in mind before I move on to mapping or imports setup?
