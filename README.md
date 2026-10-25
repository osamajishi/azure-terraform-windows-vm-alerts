# Azure Windows VM Infrastructure Provisioning with Azure Monitor Alerts using Terraform

---

## 1. Architecture & Provisioned Resources

### Core Infrastructure Topology

| Resource Type | Resource Name | Specification / Purpose | Region / Location |
| :--- | :--- | :--- | :--- |
| **Virtual Network** | `app-network` | Virtual network with `10.0.0.0/16` address space[cite: 40, 45] | East US[cite: 40, 45] |
| **Subnet** | `SubnetA` | Workload subnet with `10.0.0.0/24` address prefix[cite: 40, 45] | East US[cite: 40, 45] |
| **Network Interface** | `app-interface` | Primary network interface with dynamic IP allocation[cite: 40, 45] | East US[cite: 40, 45] |
| **Windows Virtual Machine** | `app-vm` | `Standard_B2s` VM running Windows Server 2019 Datacenter[cite: 40, 45] | East US[cite: 40, 45] |
| **Action Group** | `email-alert` | Azure Monitor Action Group configured for administrator email notifications[cite: 41, 45] | Global[cite: 39, 45] |
| **Metric Alert Rule** | `Network-Threshold-alert` | Azure Monitor metric alert triggering when Network Out Total exceeds 70 bytes[cite: 41, 45] | Global[cite: 39, 45] |

---

### Provisioned Environment Validation

![Resource Group Inventory](images/resources.png)

*Resource group inventory confirming successful deployment of Virtual Network, Subnet, Network Interface, Windows VM, Action Group, and Metric Alert Rule[cite: 39].*

---

## 2. Step-by-Step Implementation

### Step 1: Write Main Infrastructure Configuration

1. Defined Terraform provider configuration using HashiCorp `azurerm` provider[cite: 40, 45].
2. Configured networking resources including Virtual Network `app-network`, Subnet `SubnetA`, and Network Interface `app-interface`[cite: 40, 45].

![Terraform Provider and Network Code](images/terraform.png)

*VS Code editor demonstrating Terraform HCL block defining Azure provider, local variables, virtual network, and network interface resources[cite: 40].*

---

### Step 2: Define Compute and Azure Monitor Alert Resources

1. Configured `azurerm_windows_virtual_machine` resource for `app-vm` with attached OS disk and source image reference[cite: 45].
2. Created `azurerm_monitor_action_group` for email notifications and `azurerm_monitor_metric_alert` for monitoring VM network egress bytes[cite: 41, 45].

![Terraform Compute and Alert Configuration](images/terraform2.png)

*VS Code editor displaying HCL configuration for action group receivers and metric alert rule criteria targeting the virtual machine[cite: 41].*

---

### Step 3: Initialize Terraform Working Directory

1. Uploaded `main.tf` configuration file to the working directory[cite: 43].
2. Executed `terraform init` to download required provider plugins and initialize backend settings[cite: 43].

![Terraform Init Execution](images/upload-file-and-init.png)

*Terminal prompt displaying file upload confirmation and execution of terraform init command[cite: 43].*

---

### Step 4: Apply Terraform Configuration

1. Executed `terraform apply` to create and provision all defined Azure resources[cite: 42].
2. Verified automated provisioning of network components, virtual machine, and metric alert rules[cite: 39, 42, 45].

![Terraform Apply Execution](images/terraform-apply.png)

*Terminal command prompt confirming execution of terraform apply to provision cloud resources[cite: 42].*

---

## 3. Verification & Monitoring

### Endpoint Validation

1. Navigated to the Azure Portal to confirm resource creation under the specified resource group[cite: 39].
2. Verified active status of the `Network-Threshold-alert` metric alert rule connected to the `email-alert` action group[cite: 39, 41, 45].

![Resource Group Inventory](images/resources.png)

*Azure Portal resource group overview confirming active deployment and binding of metric alert rules to the virtual machine[cite: 39].*
