# ci-template-gitops

## Charts
The `charts/` directory contains charts that deploy resources for students and shared resources. The following table calls out the charts and their documentation.

| Chart | Description | Path | Example Values |
| --- | --- | --- | --- |
| Student Namespaces | Creates a shared namespace called `student-services`, and optionally creates namespaces for students according to a provided list | `charts/student-namespaces/` | [Example Values](./charts/student-namespaces/example-values.yaml) |
| Build Images RBAC | Creates the appropriate rbac for a service account to build images using the build service | `charts/build-images-rbac/` | None required |
| Build Flightctl CLI | Builds an image that has the flightctl CLI baked in, stores it in the internal registry | `charts/build-flightctl-cli/` | [Example Values](./charts/build-flightctl-cli/example-values.yaml) |
| ACM and RHEM | Installs the ACM operator, and creates an instance of MultiClusterHub with the Edge Manager preview plugin | `charts/acm-rhem/` | [Example Values](./charts/acm-rhem/example-values.yaml) |
| Pipelines | Installs the pipelines functionality onto OCP | `charts/pipelines/` | None required |
| Create Flightctl Agent Config | Creates a configmap with the flightctl agent config, useful for builds later on | `charts/create-flightctl-agent-confg/` | [Example Values](./charts/create-flightctl-agent-config/example-values.yaml) |
| Registry Auth | Creates a configmap with a registry auth file, useful for builds later on | `charts/registry-auth/` | None required |
| Bootc Image Pipeline | Creates a pipeline that builds bootc images, and imports them for OCP virtualization | `charts/bootc-image-pipeline/` | [Example Values](./charts/bootc-image-pipeline/example-values.yaml) |
| Student Virtual Machines | Creates virtual machines and supporting resources for students | `charts/student-virtual-machines/` | [Example Values](./charts/student-virtual-machines/example-values.yaml) |

## Input Values
The following is an example of all values required by all charts to deploy, as an example:
```yaml
---
gitSource:
  url: https://github.com/rhpds/lb2517-edge-fleet-gitops.git
  ref: main

advancedClusterManagement:
  storageClassName: your-storage-class-here

openshiftAuth:
  username: your-username-here
  password: your-password-here

bootcImageBuilderConfig:
  username: example-username
  password: example-password

pullSecret: 'your-pull-secret-here'

students:
  - student1
  - student2
  - student3

virtualMachines:
  storageSize: 30Gi
  storageClass: example-storage-class
  sourcePvcName: source-pvc-here
  sourcePvcNamespace: student-services
```