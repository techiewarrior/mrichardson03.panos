# PAN-OS Ansible Collection - mrichardson03.panos

![CI/CD](https://github.com/mrichardson03/mrichardson03.panos/workflows/CI/CD/badge.svg)

Ansible collection for automating configuration and operational tasks on
Palo Alto Networks Next Generation Firewalls using the PAN-OS API.

For more documentation, check the [project wiki](https://github.com/mrichardson03/mrichardson03.panos/wiki).

## How is this different than paloaltonetworks.panos?

This collection is different than the official Palo Alto Networks collection in
a number of key ways:

- **Direct XML API support.** All aspects of PAN-OS can be configured using the
  standard Ansible Jinja2 templating language.
- **Designed for customization.** Action plugins can further extend the modules
  in this collection to support complex workflows.
- **Uses standard Ansible connection methods.** This collection is written using
  as an Ansible `httpapi` plugin. This allows for a number of enhancements,
  most notably persistent connections to the device.
- **No more non-standard dependencies.** Only Python modules shipped in
  Ansible Tower are used, `xmltodict` and `requests`.

This collection is **not backwards compatible** with `paloaltonetworks.panos`.

## Installation

Install this collection using the Ansible Galaxy CLI:

```
ansible-galaxy collection install mrichardson03.panos
```

## Usage

### Sample Playbook

```
---
- hosts: fw

  collections:
    - mrichardson03.panos

  tasks:
    - name: Get system info
      panos_op:
        cmd: 'show system info'
      register: res

    - debug:
        msg: '{{ res.stdout }}'
```

Either refer to modules by their fully qualified collection name (FQCN), or use
the `collection` specification in your playbooks.

### Sample Inventory

Configuration options can be specified using host variables, like the following:

```
fw        ansible_host=192.168.55.10

[all:vars]
ansible_user=admin
ansible_password=P4loalto!

ansible_network_os=mrichardson03.panos.panos
ansible_connection=httpapi
ansible_httpapi_use_ssl=True
ansible_httpapi_validate_certs=False
```

See the [httpapi connection documentation](https://docs.ansible.com/ansible/latest/collections/ansible/netcommon/httpapi_connection.html) for the full list of options.

Authentication via API key is also supported using the variable
`ansible_api_key`.

## Python Compatability

This collection is written for Python 3.6.8, which is the version used in the
default Ansible Tower/AWX virtual environment.

## Support

This template/solution is released under an as-is, best effort, support
policy. These scripts should be seen as community supported and Palo
Alto Networks will contribute our expertise as and when possible. We do
not provide technical support or help in using or troubleshooting the
components of the project through our normal support options such as
Palo Alto Networks support teams, or ASC (Authorized Support Centers)
partners and backline support options. The underlying product used (the
VM-Series firewall) by the scripts or templates are still supported, but
the support is only for the product functionality and not for help in
deploying or using the template or script itself.

Unless explicitly tagged, all projects or work posted in our GitHub
repository (at <https://github.com/PaloAltoNetworks>) or sites other
than our official Downloads page on <https://support.paloaltonetworks.com>
are provided under the best effort policy.
