# Roboshop Catalogue Microservice - Continuous Delivery & Deployment

Welcome to the **catalogue-cd** repository. This project focuses on the continuous delivery (CD) and deployment automation for the Catalogue microservice, providing all the configurations and scripts necessary for seamless CI/CD integration, deployment to Kubernetes, and Helm-based release management.

---

## Overview

This repository contains:
- **Jenkinsfile**: Pipeline as code for automated CI/CD with Jenkins.
- **Kubernetes YAML files**: Declarative specs for deploying and managing the Catalogue microservice in Kubernetes clusters.
- **Helm charts**: Modular, reusable, and configurable Kubernetes package manager code for robust deployment and release management.
- **Jenkins Shared Library Integration**: Utilizes a centralized Jenkins shared library ([jenkins-shared-library](https://github.com/subbu20n/jenkins-shared-library)) for standardized pipeline steps and DRY (Don't-Repeat-Yourself) automation across repositories.

---

## Repository Structure

```
.
├── Jenkinsfile             # Jenkins pipeline configuration
├── helm/                   # Helm charts for the catalogue service
├── k8s/                    # Kubernetes manifests (YAML files)
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ...other manifests
└── README.md
```

---

## Features

- **Automated CI/CD**: End-to-end deployment automation using Jenkins pipelines.
- **Kubernetes-Native**: All deployments and services are described as code using K8s YAML manifests.
- **Helm-Powered Deployments**: Parameterized and environment-friendly deployments using Helm charts.
- **Modular and Reusable**: Easily adapt the pipeline and manifests for different environments and microservices.

---

## Getting Started

### Prerequisites

- [Jenkins](https://www.jenkins.io/) installed with necessary plugins (Kubernetes, Git, Helm, etc.)
- [Helm](https://helm.sh/) CLI installed
- Access to a [Kubernetes](https://kubernetes.io/) cluster

### Setup & Usage

1. **Clone the repository**
   ```bash
   git clone https://github.com/subbu20n/catalogue-cd.git
   cd catalogue-cd
   ```

2. **Configure Jenkins**
   - Import or reference the `Jenkinsfile` in your Jenkins job.
   - Set up necessary secrets/credentials for your Kubernetes cluster and Docker registry.
   - **Jenkins Shared Library**: 
     - Reference the shared library in your Jenkins global configuration or in the pipeline using the `@Library` annotation:
       ```groovy
       @Library('jenkins-shared-library') _
       ```
     - For more details and usage examples, see the [jenkins-shared-library repository](https://github.com/subbu20n/jenkins-shared-library).

3. **Helm Deployment**
   - Customize values in `helm/values.yaml` as needed.
   - Deploy using Helm:
     ```bash
     helm install catalogue helm/
     # or upgrade
     helm upgrade catalogue helm/
     ```

4. **Kubernetes Manifests**
   - Apply the manifests directly (if not using Helm):
     ```bash
     kubectl apply -f k8s/
     ```

---

## Folder Details

- **helm/**: Contains Helm chart code for templated deployments.
- **k8s/**: Raw Kubernetes manifests for deployment, service, config maps, etc.
- **Jenkinsfile**: Declarative pipeline for building, testing, and deploying the catalogue service.
- **Jenkins Shared Library**: Externalized pipeline steps, utilities, and best practices imported from [jenkins-shared-library](https://github.com/subbu20n/jenkins-shared-library).

---

## Customization

- **Helm values**: Edit `helm/values.yaml` for environment-specific configurations.
- **Manifests**: Modify or extend the YAML files under `k8s/` as required.
- **Pipeline**: Update the `Jenkinsfile` for additional stages or integrations.

---

## Contributing

Contributions, issues, and feature requests are welcome. Please fork the repo and submit pull requests for any enhancements.

---

## License

This repository is licensed under the MIT License.

---

## Maintainer

- ** SUBBU **
- GitHub: [subbu20n](https://github.com/subbu20n)