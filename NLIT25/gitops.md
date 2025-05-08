# Using GitOps to Transform Continuous Delivery into Infrastucture as Code

### What is GitOps?
- DevOps, using a Git repo as a source of truth for infra and app deployments
- Declarative, not imparative. Define state, not configuration. 
- Use software to define desired state. 
- Often paired with Kubernete
- Popular tools for GitOps w/ k8s - ArgoCD, Flux, Rancher Fleet
- Hierarchy of manifests declaring desired state (YAML, Kustomize, Helm definitions)

### Why GitOps?
- Deployment is simple - changes and rollbacks align with standard git functions
- State reconciliation helps prevent and mitigate config drift
- Built-in audit trail for infra state
- Quick scaling / recovery

### Challenges of GitOps
- Managing secrets
- Permission models

### Infrastructure Deployment
- Cloud native applications can be fully defined via GitOps --> Databases, identities, RBAC
- Tools like Terraform let entire infrastucture be defined in code

### Summary
- Requires a paradigm shift in how deployments are approached
- Usually your current deployment and release model can work with GitOps
- Saves time and effort in the long run
