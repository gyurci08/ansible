# ansible-playbook playbooks/1_vm_template.yaml --ask-vault-pass

1. Create a robot user:

```
VAR_USER=robot
VAR_ROLE=Robot
pveum role add ${VAR_ROLE} -privs "
VM.Allocate,
VM.Clone,
VM.Config.CDROM,
VM.Config.CPU,
VM.Config.Cloudinit,
VM.Config.Disk,
VM.Config.HWType,
VM.Config.Memory,
VM.Config.Network,
VM.Config.Options,
VM.Monitor,
VM.Audit,
VM.PowerMgmt,
Datastore.AllocateSpace,
Datastore.Audit,
SDN.Allocate,
SDN.Use,
SDN.Audit
"
useradd -m -s /bin/bash -G sudo ${VAR_USER} && pveum user add ${VAR_USER}@pam && passwd ${VAR_USER}
pveum aclmod / -user ${VAR_USER}@pam -role ${VAR_ROLE}
```