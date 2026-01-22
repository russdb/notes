# YOUR ROLE  
You are a Senior DevOps Architect and Municipal IT Systems Expert specializing in Red Hat OpenShift Service on AWS (ROSA). You have deep expertise in GitOps methodologies (Argo CD), Infrastructure as Code (Ansible), and US public sector compliance standards (NIST/HIPAA).  
  
# CONTEXT  
A small town in the USA needs to modernize its digital infrastructure by deploying a cloud-native platform on AWS. The town requires a cost-effective, minimal-footprint solution to host critical municipal services: Town Administration, Utility Billing, Public Records, and Health & Human Services. The environment must be strictly segmented (Production separated) and compliant with US regulations.  
  
# TASK  
Generate a comprehensive infrastructure and deployment scaffold using Ansible and Kubernetes/OpenShift manifests.  
  
# TECHNICAL SPECIFICATIONS  
1. **Platform:** AWS (ROSA - Managed OpenShift).  
- *Topology:* Minimal/Compact Cluster (3 nodes acting as control plane + worker) or Single Node (SNO) if viable for the requested services, deployed in a Single Availability Zone to minimize data transfer costs.  
2. **CI/CD & GitOps:**  
- **Argo CD:** For managing deployment of plain YAML manifests.  
- **Argo Rollouts:** For Blue/Green or Canary deployment strategies.  
3. **Infrastructure as Code (IaC):** Ansible Automation Platform (Playbooks/Roles) to provision the ROSA cluster and bootstrap the environment.  
4. **Workloads (Namespace Logic):**  
- `muni-admin` (Permits/Admin)  
- `muni-utility` (Billing)  
- `muni-records` (Archive)  
- `muni-health` (HHS - HIPAA considerations)  
5. **AI-Determined Decisions (You must implement these):**  
- **Storage:** Configure the AWS EBS CSI driver for generic persistent storage (RWO) and AWS EFS for shared public records (RWX).  
- **Identity Provider:** Integrate an OIDC provider (assume Keycloak deployed on-cluster or AWS Cognito) for centralized citizen and employee login.  
  
# STEP-BY-STEP INSTRUCTIONS  
  
## PART 1: Ansible ROSA Provisioning  
Write an Ansible Playbook (`setup_rosa.yml`) using the `redhat.openshift_managed` collection or `shell` tasks wrapping the `rosa` CLI to:  
- Create a cluster named `town-prod`.  
- Configure it as a single-zone, compact cluster (3 m5.xlarge nodes).  
- Enable cluster-admin access.  
  
## PART 2: GitOps Bootstrap (Argo CD)  
Provide the Plain YAML manifests to:  
- Install the OpenShift GitOps Operator (Argo CD).  
- Configure an `AppProject` for municipal services with strict permission boundaries.  
- Create a root `Application` (App of Apps pattern) pointing to a Git repository.  
  
## PART 3: Service Manifests & Deployment Strategies  
Provide sample Plain YAML (Deployment, Service, Route, PVC) for the **Utility Billing Service**, demonstrating:  
- **Argo Rollouts:** Use a `Rollout` resource instead of a standard Deployment to define a Canary strategy.  
- **Storage:** A PersistentVolumeClaim using the AWS EBS StorageClass.  
  
## PART 4: Compliance & Security Overlay  
Briefly document how this configuration addresses US Compliance:  
- Network Policies (deny-by-default).  
- Encryption at rest (AWS KMS integration for EBS).  
  
# CONSTRAINTS & STYLE  
- **Format:** well-commented YAML and Ansible code blocks.  
- **Manifest Strategy:** STRICTLY Plain YAML (No Helm charts or Kustomize logic in the examples, per user request).  
- **Tone:** Professional, technical, and architecturally sound.  
- **Output Language:** English.  
  
# OUTPUT FORMAT  
Provide the solution in Markdown with clear headers for "Ansible Infrastructure Code", "GitOps Configuration", "Workload Manifests", and "Compliance Notes".