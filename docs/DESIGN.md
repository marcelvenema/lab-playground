# Lab Playground platform design

- Objective: reproducible, secure, and observable VM for lab workloads.
- Base: Rocky Linux 9 on lab_network, provisioned via Ansible roles.
- Principles: idempotent roles, least-privilege secrets, immutable container runtime.

```mermaid
erDiagram
"Lab Playground Server" {
  type virtualmachine
  os rockylinux9
  network lab_network
  cpu 2_vCPU
  memory 4_GiB
  storage 50_GiB
}

"Lab Playground Server" ||--|| "base_os_config" : "01. install"
base_os_config {
  type role
  description base_operatingsystem_configuration
  action install
}

"Lab Playground Server" ||--|| "podman" : "02. install"
podman {
  type role
  description container_runtime
  action install
}

"Lab Playground Server" ||--|| "cockpit" : "03. install"
cockpit {
  type role
  description system_management_ui
  action install
}

"Lab Playground Server" ||--|| "openbao" : "04. install"
openbao {
  type role
  description secrets_management
  action install
}

"Lab Playground Server" ||--|| "openbao_integration" : "05. configure"
openbao_integration {
  type role
  description register_vm_and_bootstrap_secrets
  action configure
}

"Lab Playground Server" ||--|| "nexus_repository" : "06. install"
nexus_repository {
  type role
  description repository_management
  action install
}

"Lab Playground Server" ||--|| "monitoring" : "07. install"
monitoring {
  type role
  description metrics_and_alerting
  action install
}

"Lab Playground Server" ||--|| "logging" : "08. install"
logging {
  type role
  description centralized_logging
  action install
}

"Lab Playground Server" ||--|| "backup" : "09. configure"
backup {
  type role
  description backup_and_recovery
  action configure
}
```

```mermaid
flowchart TD
A[VM provisioned (Rocky Linux 9)] --> B[01 Base OS config]
B --> C[02 Podman]
C --> D[03 Cockpit]
D --> E[04 OpenBao]
E --> F[05 OpenBao integration]
F --> G[06 Nexus Repository]
G --> H[07 Monitoring]
H --> I[08 Logging]
I --> J[09 Backup]
```

- Notes:
  - Secrets are requested at runtime from OpenBao; no plaintext on disk.
  - Monitoring/logging export container and host metrics/logs.
  - Backups cover Nexus data and critical configs.
