
<p align="center">
   <img src="https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/images/logo-classicblue-800px.png?raw=true" alt="Intel Logo" width="250"/>
</p>

# Intel® Cloud Optimization Modules for Ansible

© Copyright 2023, Intel Corporation

## Ansible Intel Azure VM - Linux VM
This example creates an Azure Virtual Machine on Intel Icelake CPU on Linux Operating System. The virtual machine is created on an Intel Icelake Standard_D2_v5 by default.

As you configure your application's environment, choose the configurations for your infrastructure that matches your application's requirements. In this example, the virtual machine is using a preconfigured network interface, subnet, and resource group and has an additional option to enable boot diagnostics. The tags Name, Owner and Duration are added to the virtual machine when it is created.

### Explained Ansible Azure VM - Linux VM collection
This collection included 2 roles and 3 playbooks.

**Role**:- Ansible roles are a way to reuse and organize your Ansible code. They are self-contained units that contain all the files and configuration needed to automate a specific task.
Roles are defined using a directory structure with specific directories for tasks, variables, files, templates, and other artifacts. This structure makes it easy to find and reuse code, and it also makes it easy to extend behaviour of roles.

To use a role in an Ansible playbook, you simply need to list it in the roles section of the playbook. Ansible will then automatically load the role and execute its tasks.

For this module, There are 2 roles.
1. <a name="azure_rhel_vm_multi_disks"> azure_rhel_vm_multi_disks</a> - It creates multiple disks on an Azure virtual machine on Intel Icelake CPU on Linux Operating System
2. <a name="azure_rhel_vm_spot_vm"> azure_rhel_vm_spot_vm</a> creates a Spot Azure Virtual Machine on Intel Icelake CPU on Linux Operating System

**
****Playbook**:- An Ansible playbook is a YAML file that describes the tasks, are composed of a series of plays, which are groups of tasks that are executed in a specific order. Each play defines a set of tasks that should be executed on a specific group of hosts.
         Playbooks can also include variables, which can be used to store data that is used by the tasks. This makes it easy to reuse playbooks for different environments and configurations.
         for this module. 
For this module, There are 3 playbooks, Where
1. Playbook **intel_azure_linux_vm.yml** - Used to creates an Azure Virtual Machine on Intel Icelake CPU on Linux Operating System, it uses Terraform module **terraform-intel-azure-linux-vm** and being called by Ansible module community.general.terraform
2. Playbook **intel_azure_rhel_vm_multi_disks.yml** - It executes role called [azure_rhel_vm_multi_disks](#azure_rhel_vm_multi_disks)
3. Playbook **intel_azure_rhel_vm_spot_vm.yml** - It executes role called [azure_rhel_vm_spot_vm](#azure_rhel_vm_spot_vm)

```bash
.
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── galaxy.yml
├── playbooks
│   ├── intel_azure_linux_vm.yml
│   ├── intel_azure_rhel_vm_multi_disks.yml
│   └── intel_azure_rhel_vm_spot_vm.yml
├── README.md
├── requirements.txt
├── requirements.yml
├── roles
│   ├── azure_rhel_vm_multi_disks
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   ├── download_tf_module.yml
│   │   │   ├── main.yml
│   │   │   ├── managed_disk.yml
│   │   │   ├── output.yml
│   │   │   ├── read_tfstate.yml
│   │   │   └── vm.yml
│   │   ├── templates
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   └── azure_rhel_vm_spot_vm
│       ├── defaults
│       │   └── main.yml
│       ├── files
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── README.md
│       ├── tasks
│       │   ├── download_tf_module.yml
│       │   ├── main.yml
│       │   ├── output.yml
│       │   └── rhel_vm.yml
│       ├── templates
│       ├── tests
│       │   ├── inventory
│       │   └── test.yml
│       └── vars
│           └── main.yml
└── security.md

```

Requirements
------------
| Name                                                                               | Version    |
|------------------------------------------------------------------------------------|------------|
| <a name="requirement_terraform"></a> [Terraform](#requirement\_terraform)          | =1.5.7     |
| <a name="requirement_azure_cli"></a> [Azure CLI](#requirement\_azure_cli)   | ~> 2.54.0 |
| <a name="requirement_ansible_core"></a> [Ansible Core](#requirement\_ansible\_core) | ~>2.14.2   |
| <a name="requirement_ansible"></a> [Ansible](#requirement\_ansible)                | ~>7.2.0-1  |


Note:
1. Install requirements using `requirements.txt` and `requirements.yml`, Use below command:
    ```bash
    pip3 install -r requirements.txt
    ansible-galaxy install -r requirements.yml
    ```
2. Above role requires `Terraform` as we are executing terraform module [terraform-intel-azure-linux-vm](<https://github.com/intel/terraform-intel-azure-linux-vm>) using Ansible module called [community.general.terraform](<https://docs.ansible.com/ansible/latest/collections/community/general/terraform_module.html>)

## Installation of collection

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

## Authenticate Azure
1. Download and Install Azure CLI: https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=dnf
2. Authenticate Azure CLI: https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest#az-login


## Usage
Use [playbook](playbooks/intel_azure_linux_vm.yml) to execute Terraform module [terraform-intel-azure-linux-vm](<https://github.com/intel/terraform-intel-azure-linux-vm>) using Ansible module [community.general.terraform](<https://docs.ansible.com/ansible/latest/collections/community/general/terraform_module.html>) as below

```yml
- hosts: localhost
  vars:
    terraform_source: https://github.com/intel/terraform-intel-azure-linux-vm.git
  tasks:
    - set_fact:
        terraform_module_download_path: '/home/{{ansible_env.USER}}/terraform/main/intel_azure_linux_vm/'

    - name: Clone a github repository
      git:
        repo: '{{ terraform_source }}'
        dest: '{{ terraform_module_download_path }}'
        clone: yes
        update: yes
        version: main

    - name: Azure linux vm
      community.general.terraform:
        project_path: '{{ terraform_module_download_path }}'
        state: present
        force_init: true
        complex_vars: true
        # for additional variables
        # https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/variables.tf
        variables:
          azurerm_resource_group_name: "rg-intel-29112023"
          azurerm_virtual_network_name: "vnet1"
          virtual_network_resource_group_name: "rg-intel-29112023"
          virtual_machine_size: "Standard_D2s_v3"
          azurerm_subnet_name: "default"
          admin_password: "Password@123"
          tags:
            owner: user@company.com
            duration: 1
      register: vm_output

    - debug:
        var: vm_output
```
Use below Command:
```commandline
ansible-playbook intel_azure_linux_vm.yml
```

## Run Ansible with Different State
#### State - planned (terraform plan)
```yaml
- name: Azure linux vm
  community.general.terraform:
    project_path: '{{ terraform_module_download_path }}'
    state: planned
    force_init: true
    complex_vars: true
    # for additional variables
    # https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/variables.tf
    variables:
      azurerm_resource_group_name: "rg-intel-29112023"
      admin_password: "Password@123"
  register: vm_output
```

#### State - present (terraform apply)
```yaml
- name: Azure linux vm
  community.general.terraform:
    project_path: '{{ terraform_module_download_path }}'
    state: present
    force_init: true
    complex_vars: true
    # for additional variables
    # https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/variables.tf
    variables:
      azurerm_resource_group_name: "rg-intel-29112023"
      admin_password: "Password@123"
  register: vm_output
```


#### State - absent (terraform destroy)
```yaml
- name: Azure linux vm
  community.general.terraform:
    project_path: '{{ terraform_module_download_path }}'
    state: absent
    force_init: true
    complex_vars: true
    # for additional variables
    # https://github.com/intel/terraform-intel-azure-linux-vm/blob/main/variables.tf
    variables:
      azurerm_resource_group_name: "rg-intel-29112023"
      admin_password: "Password@123"
  register: vm_output
```
## See roles folder for complete examples

| Role Name                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------|
| [azure_rhel_vm_multi_disks](https://github.com/OTCShare2/ansible-intel-azure-linux-vm/tree/main/roles/azure_rhel_vm_multi_disks) |
| [azure_rhel_vm_spot_vm](https://github.com/OTCShare2/ansible-intel-azure-linux-vm/tree/main/roles/azure_rhel_vm_spot_vm)         |


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

