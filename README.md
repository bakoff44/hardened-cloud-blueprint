# 🚀 Hardened Cloud Blueprint (Hetzner / Scaleway)

An all-in-one, production-ready Infrastructure-as-Code (IaC) template to deploy a secure, highly-available micro-cluster for under **€15/month**. 

Stop overpaying for AWS/GCP managed services. Deploy your own hardened infrastructure in under 10 minutes.

---

## 🏗️ What's Included?

This repository contains fully automated **Terraform** and **Ansible** scripts designed for zero-touch deployment:

* **Provisioning (Terraform/OpenTofu)**:
  * Private Network (VPC) with automated firewall rules.
  * Pay-as-you-go cloud instances (Hetzner Cloud / Scaleway).
  * Object Storage (S3) bucket setup for automated backups.

* **Security & Hardening (Ansible)**:
  * SSH hardening (Custom ports, pubkey authentication only, root disabled).
  * Automatic security patches (`unattended-upgrades`).
  * Intruders prevention with **CrowdSec** / **Fail2ban**.

* **Orchestration & Application Stack**:
  * Lightweight Kubernetes (**k3s**) or **Docker Compose** ready for workloads.
  * **Traefik Reverse Proxy** with automated Let's Encrypt SSL certificates.

* **Observability & Backups**:
  * Automated encrypted nightly backups using **Restic** to S3 storage.
  * Pre-configured **Uptime Kuma** or Prometheus/Grafana metrics stack.

---

## 📦 Prerequisites

* [Terraform](https://www.terraform.io/) >= 1.5 (or OpenTofu)
* [Ansible](https://www.ansible.com/) >= 2.14
* An active account on Hetzner Cloud or Scaleway (API token required)

---

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone [https://github.com/your-username/hardened-cloud-blueprint.git](https://github.com/your-username/hardened-cloud-blueprint.git)
cd hardened-cloud-blueprint
```

### 2. Configure variables
Copy the example configuration files and add your API keys:

``` bash
cp terraform/terraform.tfvars.example terraform/terraform.tfvars
cp ansible/vars/all.yml.example ansible/vars/all.yml
```

3. Deploy Infrastructure
``` bash
cd terraform
terraform init
terraform apply
```

### 4. Provision & Harden
``` bash
cd ../ansible
ansible-playbook -i inventory.ini site.yml
```

🔒 Security Architecture
```
Internet ---> [ Firewall / CrowdSec ] ---> [ Traefik (HTTPS) ] ---> [ k3s / Apps ]
                                                                       |
                                                               (Nightly Restic)
                                                                       v
                                                               [ S3 Bucket Storage ]
```
### 📄 License
Distributed under the MIT License. See LICENSE for more information.
