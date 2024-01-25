<p align="center">
   <img src="https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/images/logo-classicblue-800px.png?raw=true" alt="Intel Logo" width="250"/>
</p>

# Intel® Cloud Optimization Modules for Ansible

© Copyright 2022, Intel Corporation

## Ansible Intel Azure VM - Linux VM Creating Multiple Disks

This example creates multiple disks on an Azure virtual machine on Intel Icelake CPU on Linux Operating System. The virtual machine is created on an Intel Icelake Standard_D2_v5 by default.

As you configure your application's environment, choose the configurations for your infrastructure that matches your application's requirements.

In this example, the virtual machine is using a preconfigured network interface, subnet, and resource group. The tags Name, Owner and Duration are added to the virtual machine when it is created.

## Authenticate Azure
1. Download and Install Azure CLI: https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=dnf
2. Authenticate Azure CLI: https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest#az-login

## Installation of `azure_rhel_vm_multi_disks` role
### Below are ways to install and use it:

1. **Case 1:-** When user's needs can be met with the default configuration, and they want to install a collection 
   from Ansible Galaxy to the default location (as a third-party collection), it is recommended to use the following command:
    ```commandline
        ansible-galaxy  collection install <ansible-intel-azure-linux-vm>
    ```
   
2. **Case 2:-** When user's needs can't be met with the default configuration, wants to extend/modify existing configuration and flow, They can install collection using Ansible Galaxy in user's define location
   Use below approaches

   1.
       ```commandline
       ansible-galaxy  collection install -p <local path> <ansible-intel-azure-linux-vm>
       ```
       Note: collection will download collection, you can remove as per need

   2. Download source and Copy role directory to your Ansible boilerplate  from GitHub (Used to extended behavior of role)  
       ```commandline
       git clone https://github.com/OTCShare2/ansible-intel-azure-linux-vm.git
       cd ansible-intel-azure-linux-vm
       cp -r role/azure_rhel_vm_multi_disks /<your project path>/
       ``` 

Requirements
------------
| Name                                                                                | Version   |
|-------------------------------------------------------------------------------------|-----------|
| <a name="requirement_terraform"></a> [Terraform](#requirement\_terraform)           | =1.5.7    |
| <a name="requirement_azure_cli"></a> [Azure CLI](#requirement\_azure_cli)           | ~> 2.54.0 |
| <a name="requirement_ansible_core"></a> [Ansible Core](#requirement\_ansible\_core) | ~>2.14.2  |
| <a name="requirement_ansible"></a> [Ansible](#requirement\_ansible)                 | ~>7.2.0-1 |

Note:
1. Install requirements using `requirements.txt` and `requirements.yml`, Use below command:
    ```bash
    pip3 install -r requirements.txt
    ansible-galaxy install -r requirements.yml
    ```
2. Above role requires `Terraform` as we are executing terraform module [terraform-intel-azure-linux-vm](<https://github.com/intel/terraform-intel-azure-linux-vm>) using Ansible module called [community.general.terraform](<https://docs.ansible.com/ansible/latest/collections/community/general/terraform_module.html>)

## Usage
Use playbook to run azure_rhel_vm_multi_disks as below
```yml
---
- name: Run azure_rhel_vm_multi_disks role
  hosts: localhost
  tasks:
    - name: Running a role Azure linux vm multi disks
      ansible.builtin.import_role:
        name: azure_rhel_vm_multi_disks
      vars:
        rhel_vm_state: present
        azurerm_resource_group_name: "<azurerm_resource_group_name>"
        virtual_network_resource_group_name: "<virtual_network_resource_group_name>"
```
Use below Command:
```commandline
ansible-playbook intel_azure_rhel_vm_multi_disks.yml
```

## Run Ansible with different state
#### State - present (terraform apply)
```yaml
---
- name: Run azure_rhel_vm_multi_disks role
  hosts: localhost
  tasks:
    - name: Running a role Azure linux vm multi disks
      ansible.builtin.import_role:
        name: azure_rhel_vm_multi_disks
      vars:
        rhel_vm_state: present
        azurerm_resource_group_name: "<azurerm_resource_group_name>"
        virtual_network_resource_group_name: "<virtual_network_resource_group_name>"
```
Use below Command:
```commandline
ansible-playbook intel_azure_rhel_vm_multi_disks.yml
```

#### State - absent (terraform destroy)
```yaml
---
- name: Run azure_rhel_vm_multi_disks role
  hosts: localhost
  tasks:
    - name: Running a role Azure linux vm multi disks
      ansible.builtin.import_role:
        name: azure_rhel_vm_multi_disks
      vars:
        rhel_vm_state: absent
        azurerm_resource_group_name: "<azurerm_resource_group_name>"
        virtual_network_resource_group_name: "<virtual_network_resource_group_name>"
```
Use below Command:
```commandline
ansible-playbook intel_azure_rhel_vm_multi_disks.yml
```

### Terraform Modules
| Name                                                                                                  |
|-------------------------------------------------------------------------------------------------------|
| [terraform-intel-azure-linux-vm](<https://github.com/intel/terraform-intel-azure-linux-vm/tree/main>) |

# Ansible

## Module State Inputs

| Name                                                                         | Description                                                                               | Type     | Default   | Required |
|------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|----------|-----------|:--------:|
| <a name="input_rhel_vm_state"></a> [rhel_vm_state](#input\_rhel_vm_state) | It specifices vm state of given stage, choies: "planned", "present" ← (default), "absent" | `string` | `present` |    no    |

## Azure Managed Disk Exposed Inputs
| Name                                                                                                      | Description                                                                                                                                                      | Type    | Default                                           | Required |
|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|---------------------------------------------------|:--------:|
| <a name="input_disk_name"></a> [disk_name](#input_disk_name)                                              | Name of the managed disk.                                                                                                                                        | `string` | `"managed_disk_name"`                             |    no    |
| <a name="input_resource_group_name"></a> [disk_resource_group_name](#input_resource_group_name)   | Name of a resource group where the managed disk exists or will be created.                                                                                       | `string` | `rg-intel-<xxxxxx>`                               |    no    |
| <a name="input_storage_account_type"></a> [storage_account_type](#input_storage_account_type) | Type of storage for the managed disk.                                                                                                                            | `string` | `"Standard_LRS"`                                  |    no    |
| <a name="input_location"></a> [location](#input_location)                         | Valid Azure location. Defaults to location of the resource group.                                                                                                | `string` | `"eastus"`                                        |    no    |
| <a name="input_create_option"></a> [create_option](#input_create_option)                                  | import from a VHD file in source_uri and copy from previous managed disk source_uri. Choices: "empty", "import", "copy"                                          | `string` | `"empty"`                                         |    no    |
| <a name="input_disk_size_gb"></a> [disk_size_gb](#input_disk_size_gb)                                     | Size in GB of the managed disk to be created.                                                                                                                    | `string` | `"8"`                                             |    no    |
| <a name="input_disk_tags"></a> [disk_tags](#input_disk_tags)                                              | Dictionary of string:string pairs to assign as metadata to the object.                                                                                           | `{}`    | `{ "owner": "user@company.com", "duration": "1"}` |    no    |
| <a name="input_lun"></a> [lun](#input_lun)                                                                | The logical unit number for data disk. This value is used to identify data disks within the VM and therefore must be unique for each data disk attached to a VM. | `string` | `10`                                              |    no    |
| <a name="input_caching"></a> [caching](#input_caching)                                                    | Disk caching policy controlled by VM. Will be used when attached to the VM defined by managed_by                                                                 | `string` | `"read_write"`                                    |    no    |

## Azure VM Exposed Inputs

| Name                                                                                                                                                  | Description                                                                           | Type       | Default                                     | Required |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|------------|---------------------------------------------|:--------:|
| <a name="input_admin_password0"></a> [admin\_password](#input\_admin\_password0)                                                                      | The Password which should be used for the local-administrator on this virtual machine | `string`   | `"Password@123"`                            |    no    |
| <a name="input_azurerm_resource_group_name0"></a> [azurerm\_resource\_group\_name](#input\_azurerm\_resource\_group\_name0)                           | Name of the resource group to be imported                                             | `string`   | `rg-intel-<xxxxxx>`                         |    no    |
| <a name="input_azurerm_subnet_name0"></a> [azurerm\_subnet\_name](#input\_azurerm\_subnet\_name0)                                                     | The name of the preconfigured subnet                                                  | `string`   | `default`                                   |    no    |
| <a name="input_azurerm_virtual_network_name0"></a> [azurerm\_virtual\_network\_name](#input\_azurerm\_virtual\_network\_name0)                        | Name of the preconfigured virtual network                                             | `string`   | `vnet1`                                     |    no    |
| <a name="input_virtual_network_resource_group_name0"></a> [virtual\_network\_resource\_group\_name](#input\_virtual\_network\_resource\_group\_name0) | Name of the resource group of the virtual network                                     | `string`   | `rg-intel-<xxxxxx>`                         |    no    |
| <a name="input_source_image_reference_offer0"></a> [source\_image\_reference\_offer](#input\_source\_image\_reference\_offer0)                        | Specifies the offer of the image used to create the virtual machine                   | `string`   | `"RHEL"`                                    |    no    |
| <a name="input_source_image_reference_publisher0"></a> [source\_image\_reference\_publisher](#input\_source\_image\_reference\_publisher0)            | Specifies the publisher of the image used to create the virtual machine               | `string`   | `"RedHat"`                                  |    no    |
| <a name="input_source_image_reference_sku0"></a> [source\_image\_reference\_sku](#input\_source\_image\_reference\_sku0)                              | Specifies the SKU of the image used to create the virtual machine                     | `string`   | `"8-LVM-gen2"`                              |    no    |
| <a name="input_source_image_reference_version0"></a> [source\_image\_reference\_version](#input\_source\_image\_reference\_version0)                  | Specifies the version of the image used to create the virtual machine                 | `string`   | `"latest"`                                  |    no    |
| <a name="input_virtual_machine_size0"></a> [virtual\_machine\_size](#input\_virtual\_machine\_size0)                                                  | The SKU that will be configured for the provisioned virtual machine                   | `string`   | `"Standard_D2s_v5"`                         |    no    |
| <a name="input_vm_tags"></a> [vm_tags](#input\_vm_tags)                                                                                               | A mapping of tags to assign to the resource                                           | `map(any)` | `{"owner":"user@company.com","duration":1}` |    no    |


## VM Terraform Extended Inputs
 Below Input variables can be used to extend variables in role, Add or update variable in vars/main.yml file
### Usage

roles/azure_rhel_vm_multi_disks/vars/main.yml
```yaml
vm_name: "new-demo"
```

roles/azure_rhel_vm_multi_disks/tasks/rhel_vm.yml
```yaml
---
- name: Azure rhel VM creation
  community.general.terraform:
    project_path: '{{ azure_vm_tf_module_download_path }}'
    state: '{{ rhel_vm_state }}'
    force_init: true 
    complex_vars: true 
    variables:
      azurerm_resource_group_name: '{{ azurerm_resource_group_name }}'
      azurerm_virtual_network_name: '{{ azurerm_virtual_network_name }}'
      virtual_network_resource_group_name: '{{ virtual_network_resource_group_name }}'
      azurerm_subnet_name: '{{ azurerm_subnet_name }}'
      admin_password: '{{ admin_password }}'
      source_image_reference_offer: '{{ source_image_reference_offer }}'
      source_image_reference_sku: '{{ source_image_reference_sku }}'
      source_image_reference_publisher: '{{ source_image_reference_publisher }}'
      source_image_reference_version: '{{ source_image_reference_version }}'
      tags: '{{ vm_tags }}'
      virtual_machine_size: '{{ virtual_machine_size }}'
      vm_name: '{{ vm_name }}'
  register: rhel_vm_output
```

Use `vm_name` in playbook
```yaml
---
- name: Run azure_rhel_vm_multi_disks role
  hosts: localhost
  tasks:
    - name: Running a role Azure linux vm multi disks
      ansible.builtin.import_role:
        name: azure_rhel_vm_multi_disks
      vars:
        rhel_vm_state: absent
        vm_name: '<vm_name>'
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_admin_password"></a> [admin\_password](#input\_admin\_password) | The Password which should be used for the local-administrator on this virtual machine | `string` | n/a | yes |
| <a name="input_admin_ssh_key"></a> [admin\_ssh\_key](#input\_admin\_ssh\_key) | n/a | `list(any)` | `[]` | no |
| <a name="input_admin_username"></a> [admin\_username](#input\_admin\_username) | The username of the local administrator used for the virtual machine | `string` | `"adminuser"` | no |
| <a name="input_azurerm_network_interface_name"></a> [azurerm\_network\_interface\_name](#input\_azurerm\_network\_interface\_name) | The name of the network interface. Changing this forces a new resource to be created | `string` | `"nic1"` | no |
| <a name="input_azurerm_resource_group_name"></a> [azurerm\_resource\_group\_name](#input\_azurerm\_resource\_group\_name) | Name of the resource group to be imported | `string` | n/a | yes |
| <a name="input_azurerm_storage_account_name"></a> [azurerm\_storage\_account\_name](#input\_azurerm\_storage\_account\_name) | The name of the storage account to be used for the boot\_diagnostic | `string` | `null` | no |
| <a name="input_azurerm_subnet_name"></a> [azurerm\_subnet\_name](#input\_azurerm\_subnet\_name) | The name of the preconfigured subnet | `string` | n/a | yes |
| <a name="input_azurerm_virtual_network_name"></a> [azurerm\_virtual\_network\_name](#input\_azurerm\_virtual\_network\_name) | Name of the preconfigured virtual network | `string` | n/a | yes |
| <a name="input_disable_password_authentication"></a> [disable\_password\_authentication](#input\_disable\_password\_authentication) | Boolean that determines if password authentication will be disabled on this virtual machine | `bool` | `false` | no |
| <a name="input_disk_size_gb"></a> [disk\_size\_gb](#input\_disk\_size\_gb) | The size of the internal OS disk in GB, if you wish to vary from the size used in the image this virtual machine is sourced from | `string` | `null` | no |
| <a name="input_enable_boot_diagnostics"></a> [enable\_boot\_diagnostics](#input\_enable\_boot\_diagnostics) | Boolean that determines if the boot diagnostics will be enabled on this virtual machine | `bool` | `true` | no |
| <a name="input_eviction_policy"></a> [eviction\_policy](#input\_eviction\_policy) | Specifies what should happen when the Virtual Machine is evicted for price reasons when using a Spot instance. Possible values are Deallocate and Delete | `string` | `"Deallocate"` | no |
| <a name="input_identity"></a> [identity](#input\_identity) | n/a | <pre>object({<br>    identity_ids = optional(list(string))<br>    principal_id = optional(string)<br>    tentant_id   = optional(string)<br>    type         = optional(string, "SystemAssigned")<br>  })</pre> | `{}` | no |
| <a name="input_ip_configuration_name"></a> [ip\_configuration\_name](#input\_ip\_configuration\_name) | A name for the IP with the network interface configuration | `string` | `"internal"` | no |
| <a name="input_ip_configuration_private_ip_address_allocation"></a> [ip\_configuration\_private\_ip\_address\_allocation](#input\_ip\_configuration\_private\_ip\_address\_allocation) | The allocation method used for the private IP address. Possible values are Dynamic and Static | `string` | `"Dynamic"` | no |
| <a name="input_ip_configuration_public_ip_address_id"></a> [ip\_configuration\_public\_ip\_address\_id](#input\_ip\_configuration\_public\_ip\_address\_id) | Reference to a public IP address for the NIC | `string` | `null` | no |
| <a name="input_max_bid_price"></a> [max\_bid\_price](#input\_max\_bid\_price) | The maximum price you're willing to pay for this virtual machine, in US Dollars; which must be greater than the current spot price. If this bid price falls below the current spot price the virtual machine will be evicted using the eviction\_policy | `string` | `"-1"` | no |
| <a name="input_os_disk_caching"></a> [os\_disk\_caching](#input\_os\_disk\_caching) | The type of caching which should be used for the internal OS disk. Possible values are 'None', 'ReadOnly' and 'ReadWrite' | `string` | `"ReadWrite"` | no |
| <a name="input_os_disk_name"></a> [os\_disk\_name](#input\_os\_disk\_name) | The name which should be used for the internal OS disk | `string` | `"disk1"` | no |
| <a name="input_os_disk_storage_account_type"></a> [os\_disk\_storage\_account\_type](#input\_os\_disk\_storage\_account\_type) | The type of storage account which should back this the internal OS disk. Possible values include Standard\_LRS, StandardSSD\_LRS and Premium\_LRS | `string` | `"Premium_LRS"` | no |
| <a name="input_priority"></a> [priority](#input\_priority) | Specifies the priority of this virtual machine. Possible values are Regular and Spot. Defaults to Regular | `string` | `"Regular"` | no |
| <a name="input_route_tables_ids"></a> [route\_tables\_ids](#input\_route\_tables\_ids) | A map of subnet name for the route table ids | `map(string)` | `{}` | no |
| <a name="input_source_image_reference_offer"></a> [source\_image\_reference\_offer](#input\_source\_image\_reference\_offer) | Specifies the offer of the image used to create the virtual machine | `string` | `"0001-com-ubuntu-server-jammy"` | no |
| <a name="input_source_image_reference_publisher"></a> [source\_image\_reference\_publisher](#input\_source\_image\_reference\_publisher) | Specifies the publisher of the image used to create the virtual machine | `string` | `"Canonical"` | no |
| <a name="input_source_image_reference_sku"></a> [source\_image\_reference\_sku](#input\_source\_image\_reference\_sku) | Specifies the SKU of the image used to create the virtual machine | `string` | `"22_04-lts-gen2"` | no |
| <a name="input_source_image_reference_version"></a> [source\_image\_reference\_version](#input\_source\_image\_reference\_version) | Specifies the version of the image used to create the virtual machine | `string` | `"latest"` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | A mapping of tags to assign to the resource | `map(any)` | `{}` | no |
| <a name="input_virtual_machine_size"></a> [virtual\_machine\_size](#input\_virtual\_machine\_size) | The SKU that will be configured for the provisioned virtual machine | `string` | `"Standard_D2s_v5"` | no |
| <a name="input_virtual_network_resource_group_name"></a> [virtual\_network\_resource\_group\_name](#input\_virtual\_network\_resource\_group\_name) | Name of the resource group of the virtual network | `string` | n/a | yes |
| <a name="input_vm_name"></a> [vm\_name](#input\_vm\_name) | The unique name of the Linux virtual machine | `string` | `"vm1"` | no |
| <a name="input_write_accelerator_enabled"></a> [write\_accelerator\_enabled](#input\_write\_accelerator\_enabled) | Should write accelerator be enabled for this OS disk? Defaults to false | `bool` | `false` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_admin_username"></a> [admin\_username](#output\_admin\_username) | Virtual machine admin username |
| <a name="output_identity"></a> [identity](#output\_identity) | Identity configuration associated with the virtual machine |
| <a name="output_location"></a> [location](#output\_location) | Location where the virtual machine will be created |
| <a name="output_name"></a> [name](#output\_name) | Virtual machine name |
| <a name="output_network_interface_ids"></a> [network\_interface\_ids](#output\_network\_interface\_ids) | List of network interface IDs that are attached to the virtual machine |
| <a name="output_os_disk"></a> [os\_disk](#output\_os\_disk) | Disk properties that are attached to the virtual machine |
| <a name="output_resource_group_name"></a> [resource\_group\_name](#output\_resource\_group\_name) | Name of the resource group |
| <a name="output_size"></a> [size](#output\_size) | The SKU for the virtual machine |
| <a name="output_storage_account_tier"></a> [storage\_account\_tier](#output\_storage\_account\_tier) | Tier to identify the storage account associated with the virtual machine |
| <a name="output_tags"></a> [tags](#output\_tags) | Tags that are assigned to the virtual machine |
| <a name="output_virtual_machine_id"></a> [virtual\_machine\_id](#output\_virtual\_machine\_id) | ID assigned to the virtual machine after it has been created |
<!-- END_TF_DOCS -->