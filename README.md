# OCI VM Automation

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Platform](https://img.shields.io/badge/platform-Oracle%20Cloud-orange)
![License](https://img.shields.io/badge/license-MIT-blue)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-green)

A comprehensive automation suite for provisioning, configuring, and managing Virtual Machines (Compute Instances) on **Oracle Cloud Infrastructure (OCI)**. This repository streamlines the infrastructure lifecycle using **[Insert Tool: e.g., Terraform / Ansible / Python SDK]**.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📖 Overview

This project reduces manual overhead by automating the deployment of OCI Compute resources. It is designed to be modular, secure, and scalable, suitable for both development environments and production workloads.

**Key capabilities include:**
- Automated VCN and Subnet discovery/creation.
- Dynamic injection of SSH keys and Cloud-Init scripts.
- Attachment of block storage volumes.
- Automatic association with Network Security Groups (NSGs).

---

## ✨ Features

- **Infrastructure as Code:** Fully declarative setup for reproducible environments.
- **Multi-OS Support:** Supports Oracle Linux, Ubuntu, CentOS, and Windows images.
- **Security First:** Enforces least-privilege principles via IAM policies and strict Security Lists.
- **Custom Bootstrapping:** Supports `user_data` for post-provisioning configuration (installing Docker, updates, etc.).
- **Flexible Scaling:** Easily adjust OCPUs and Memory for Flex shapes.

---

## 🏗 Architecture

> **Note:** Replace the link below with your actual architecture diagram.

![Architecture Diagram](https://via.placeholder.com/800x400?text=OCI+Architecture+Diagram+Placeholder)

The automation creates the following resources:
1. **Networking:** VCN, Public/Private Subnets, Internet Gateway/NAT Gateway.
2. **Compute:** VM instances using flexible shapes (e.g., `VM.Standard.E4.Flex`).
3. **Storage:** Boot volumes and optional attached Block Volumes.

---

## ✅ Prerequisites

Before running the automation, ensure you have the following:

1. **Oracle Cloud Account:** A generic active OCI account.
2. **OCI API Keys:** An RSA key pair in PEM format for API signing.
   - [Documentation: How to generate API keys](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)
3. **Required Tools:**
   - [CLI Tool Name, e.g., Terraform v1.0+]
   - [CLI Tool Name, e.g., OCI CLI]
   - Git

---

## ⚙️ Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/OCI-vm-automation.git
   cd OCI-vm-automation
   ```

2. **Initialize Dependencies**
   *If using Terraform:*
   ```bash
   terraform init
   ```
   *If using Python:*
   ```bash
   pip install -r requirements.txt
   ```

---

## 🔧 Configuration

Copy the example configuration file to create your local settings file.

```bash
cp examples/terraform.tfvars.example terraform.tfvars
# OR
cp config.example.yaml config.yaml
```

### Key Variables

| Variable | Description | Required | Default |
| :--- | :--- | :---: | :--- |
| `tenancy_ocid` | The OCID of your tenancy | Yes | - |
| `user_ocid` | The OCID of the user executing the script | Yes | - |
| `fingerprint` | Fingerprint for the API signing key | Yes | - |
| `region` | OCI Region (e.g., `us-ashburn-1`) | Yes | `us-ashburn-1` |
| `compartment_id` | Target compartment for resources | Yes | - |
| `instance_shape` | VM Shape (e.g., `VM.Standard.E4.Flex`) | No | `VM.Standard.E4.Flex` |
| `ssh_public_key` | Path to your SSH public key | Yes | `~/.ssh/id_rsa.pub` |

---

## 🚀 Usage

### 1. Plan the Deployment
Preview the changes before applying them to your OCI tenancy.

```bash
# Example for Terraform
terraform plan
```

### 2. Apply Changes
Provision the infrastructure.

```bash
# Example for Terraform
terraform apply --auto-approve
```

### 3. Connect to VM
Once provisioned, the output will display the public IP.

```bash
ssh -i ~/.ssh/id_rsa opc@<PUBLIC_IP_ADDRESS>
```

### 4. Cleanup / Destroy
To remove all resources created by this automation:

```bash
terraform destroy
```

---

## ❓ Troubleshooting

**Issue: `401 Authorization failed`**
- *Cause:* Incorrect API Key, Fingerprint, or User OCID.
- *Fix:* Verify your `~/.oci/config` or your environment variables. Ensure the public key is uploaded to the User console in OCI.

**Issue: `Service Limit Reached`**
- *Cause:* Your tenancy has hit the limit for Always Free or standard Compute cores.
- *Fix:* Request a limit increase in the OCI Console or switch to a paid instance shape.

**Issue: `Invalid Parameter - ShapeConfig`**
- *Cause:* Trying to set memory/OCPU for a non-Flex shape.
- *Fix:* Only specify memory/cpu config if using E3/E4/A1 Flex shapes.

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 📞 Contact

Project Maintainer - [Your Name] - [your.email@example.com]

Project Link: [https://github.com/your-username/OCI-vm-automation](https://github.com/your-username/OCI-vm-automation)