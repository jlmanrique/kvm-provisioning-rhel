## Execute
***
There are two scripts for provision, one for provision just only one vm and the other to provision many
```
$ git clone https://github.com/jlmanrique/kvm-provisioning-rhel.git
$ ansible-playbook -K kvm_provision_new.yaml
$ ansible-playbook -K kvm_provision_many_servers.yaml
```
