## Bootstrap

Creates ansible user and installs desired packages to somothly run ansible for desired hosts. Add public key (ansible_rsa.pub) to `roles/bootstrap/files` and specify private key in the `ansible.cfg`.


`cat /etc/ansible/ansible.cfg`

```
[defaults]
roles_path = roles
remote_user = ansible
private_key_file = /path/to/.ssh/ansible_rsa

[privilege_escalation]
become=True
become_user=root

[ssh_connection]
pipelining = True
```

Run following command. Replace IP with desired host and USER with user that has access to the host. You will be asked for become password (root password).

```
ansible-playbook bootstrap.yaml -u <USER> -e target=<IP>  --ask-become-pass -i <IP>,
```

To setup docker and yellifin run following command.
```
ansible-playbook banas.yaml -e target=banas -i inventory.yaml
```