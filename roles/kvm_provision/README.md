Role Name
=========

A role for kvm provisioning.

Requirements
------------

None.

Role Variables
--------------

base_image_name: Path of the qcow file for RHEL
libvirt_pool_dir: Directory of the virtual VMs
vm_name: Name of the VM
vm_vcpus: Number of vCPUs
vm_ram_mb: Number of RAM
vm_net: KVM 
vm_root_pass: Set the root password
cleanup_tmp: Requires temporal cleaning (true or false)
ssh_key: Path of the SSH key

Dependencies
------------

None.

Example Playbook
----------------

Deploy a single VM:

- name: Deploy RHEL VM based on local image
  hosts: localhost
  gather_facts: yes
  become: yes
  vars:
    pool_dir: "/var/lib/libvirt/images"
    vm: RHEL-lab01
    vcpus: 1
    ram_mb: 1024
    cleanup: yes
    net: default
    ssh_pub_key: "/home/jlmanrique/.ssh/id_rsa.pub"

  tasks:
    - name: KVM Provision role
      include_role:
        name: kvm_provision
      vars:
        libvirt_pool_dir: "{{ pool_dir }}"
        vm_name: "{{ vm }}"
        vm_vcpus: "{{ vcpus }}"
        vm_ram_mb: "{{ ram_mb }}"

Deploy multiple VMs:

- name: Deploy RHEL VMs based on local image
  hosts: localhost
  gather_facts: yes
  become: yes
  vars:
    pool_dir: "/var/lib/libvirt/images"
    vcpus: 1
    ram_mb: 1024
    cleanup: false
    net: default
    ssh_pub_key: "/home/jlmanrique/.ssh/id_rsa.pub"
  tasks:
    - name: KVM Provision role
      include_role:
        name: kvm_provision
      vars:
        libvirt_pool_dir: "{{ pool_dir }}"
        vm_name: "{{ item }}"
        vm_vcpus: "{{ vcpus }}"
        vm_ram_mb: "{{ ram_mb }}"
        vm_net: "{{ net }}"
        cleanup_tmp: "{{ cleanup }}"
        ssh_key: "{{ ssh_pub_key }}"
      loop:
        - rhel-lab01
        - rhel-lab02
        - rhel-lab03

License
-------

BSD

Author Information
------------------

Twitter: @jlmanrique
Github: jlmanrique
