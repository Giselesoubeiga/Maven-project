EKS Automation:

Built and containerized application scripts, created Docker images, and pushed them to ECR.

Deployed workloads to EKS using YAML manifests and ensured proper networking via private subnets and NAT gateways.

Security & Access Control:

Implemented IAM OIDC roles and service accounts to limit S3 and database access to authorized pods only.

Configured security groups and IAM policies for least-privilege access across all environments.

CloudFormation Implementation:

Developed and refined CloudFormation templates for VPCs, subnets, IAM roles, and EKS components.

Standardized infrastructure provisioning to make deployments consistent and reproducible.

Jenkins Integration:

Began automating the build-and-deploy process using Jenkins pipelines.

Planned a two-stage flow: one job to build and push Docker images, and another to deploy to EKS through Ansible/YAML.

Testing & Validation:

Verified database connectivity and secure S3 uploads within EKS.

Tested working Python scripts (Misattributed & T-Value reports) within the EKS cluster to validate container performance.

Quarter-End Goals:

Finalize CloudFormation templates.

Complete Jenkins-to-EKS automation pipeline.
