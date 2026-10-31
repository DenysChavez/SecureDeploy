# SecureDeploy: Scope (v0.1)

## Problem
Security problems, such as leaving admin ports open to the internet, storing data without encryption, or allowing too much network access, can be built into infrastructure code before it is deployed. Small teams often don't have automated tools to check for these problems before applying the code. As a result, security issues may only be discovered later, or may never be noticed at all.

## Who it's for
- **Primary:** solo developers and small teams (roughly 2–10 people) who
  manage cloud infrastructure with Terraform or OpenTofu and have no
  dedicated security team.
- **Secondary:** this is also a learning and portfolio project.

## In scope
A small example infrastructure configuration (Terraform/OpenTofu, AWS
  resources) used as the system under test
- Static scanning with an off-the-shelf tool (Checkov or Trivy)
- 3–5 custom policies written with OPA/Conftest, starting with:
  - No administrative ports (SSH 22, RDP 3389) open to the internet
  - Storage must be encrypted
  - No overly permissive network rules (all ports or protocols from anywhere)
- Test fixtures: known-insecure configurations that must fail, and
  compliant configurations that must pass
- A GitHub Actions pipeline that runs all checks on every pull request and
  blocks merging when a critical policy is violated
- Documentation: setup, architecture, threat model, and an explanation of
  each policy

## Out of scope (for now)
- Deploying to a real cloud account (deferred to optional Phase 7)
- Monitoring live infrastructure or detecting runtime threats
- Scanning application code, container images, or dependencies
- Cloud providers other than AWS, and IaC formats other than
  Terraform/OpenTofu (e.g., CloudFormation, Pulumi, Kubernetes manifests)
- A web dashboard or user interface
- Automatically fixing insecure code
- Any claim of production readiness

## Assumptions and limitations
- Checks run *before* deployment. They reduce risk; they do not prove the
  deployed infrastructure is secure.
- Until Phase 7, the example infrastructure is validated and planned, never
  applied.


## Done looks like (v0.1)
- [ ] A fresh clone can be set up by following the README on macOS and Linux
- [ ] Every insecure fixture is rejected with a message explaining the
      violation and how to fix it
- [ ] Every compliant fixture passes
- [ ] Policy tests run automatically and pass
- [ ] A pull request introducing an insecure change is blocked by CI, and
      the corrected version passes
- [ ] Known limitations are documented