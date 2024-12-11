# shift-left-k8s
Open source security controls for a k8s vulnerable cluster

This repository demonstrates a CI/CD pipeline that addresses multiple categories of the Kubernetes Threat Matrix by leveraging popular tools and best practices. It is designed to emulate real-world Kubernetes environments and showcases how to secure Kubernetes clusters against common security threats.

## Pipeline Overview

This GitHub Actions pipeline:

1. Sets up a local Kubernetes cluster using [KinD (Kubernetes in Docker)](https://kind.sigs.k8s.io/).
2. Deploys the Kubernetes Goat project to simulate real-world vulnerabilities.
3. Uses a variety of tools to scan and secure the Kubernetes environment.
4. Maps security checks to categories of the Kubernetes Threat Matrix.

## Tools Used

| Tool         | Purpose                                                                 |
|--------------|-------------------------------------------------------------------------|
| **KinD**     | Sets up a local Kubernetes cluster to emulate real-world environments. |
| **Helm**     | Deploys applications and manages Kubernetes manifests.                 |
| **kubectl**  | Manages and inspects Kubernetes resources.                             |
| **Kyverno**  | Enforces RBAC and security policies.                                   |
| **kube-score** | Performs static analysis on Kubernetes manifests.                     |
| **Trivy**    | Scans for vulnerabilities in container images and file systems.        |
| **Falco**    | Detects runtime threats and anomalous behaviors in Kubernetes.         |

## Pipeline Steps

1. **Cluster Setup:**
   - Installs KinD and creates a local Kubernetes cluster named `goat-cluster`.
   - Installs and configures essential Kubernetes tools: `kubectl` and `Helm`.

2. **Application Deployment:**
   - Clones the Kubernetes Goat repository to simulate real-world vulnerabilities.
   - Deploys Kubernetes Goat scenarios using Helm and `kubectl`.

3. **Security Analysis:**
   - **Static Analysis:** Scans YAML manifests using `kube-score` for best practices.
   - **Image and File Vulnerability Scans:** Uses `Trivy` to identify critical vulnerabilities.
   - **Runtime Threat Detection:** Uses `Falco` to monitor runtime behaviors and detect threats.

4. **Reporting:**
   - Outputs reports for each tool:
     - `kube-score` static analysis report.
     - `Trivy` vulnerability scan report.
     - Processed Falco logs for critical runtime threats.
   - Artifacts are uploaded for further inspection.

## Kubernetes Threat Matrix Mapping

The pipeline addresses the following categories in the Kubernetes Threat Matrix:

| Category               | Technique                           | Tool Used          | Description                                                             |
|------------------------|-------------------------------------|--------------------|-------------------------------------------------------------------------|
| **Privilege Escalation**| Exploit Misconfigured RBAC        | Kyverno            | Enforces RBAC policies to prevent privilege escalation.                 |
| **Defense Evasion**     | Exploit Legitimate Tools          | Falco              | Detects anomalous runtime behaviors evading detection.                  |
| **Credential Access**   | Harvest Kubernetes Secrets        | kube-score         | Identifies exposed secrets in YAML manifests.                           |
| **Discovery**           | List Kubernetes Resources         | kubectl            | Displays common discovery tactics attackers might employ.               |
| **Lateral Movement**    | Use Kubernetes API                | kubectl + Helm     | Demonstrates how attackers exploit the Kubernetes API.                  |
| **Impact**              | Data Destruction via Misconfigured Pods | Trivy       | Identifies misconfigurations leading to potential destructive activities.|

## Getting Started

### Prerequisites

- A GitHub account with access to Actions.
- Understanding of Kubernetes and GitHub Actions.

### Running the Pipeline

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo-directory>
