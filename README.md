# Ansible playbook

Here a collection of ansible playbooks.
They are collected in random order.

## Run ansible playbooks

Run standard playbook, asking for remote password, using hostlist file

```shell
ansible-playbook -k -i hostsfile playbook.yml
```

Run playbook asking a password to decrypt the vault

```shell
ansible-playbook -k --vault-id @prompt -i hostsfile playbook.yml
```

Run playbook with a subset of hosts in the inventory

```shell
ansible-playbook -k --vault-id @prompt -i hostsfile -l hosts_subset_tag playbook.yml
```

## Encrypt a value for ansible vault

```shell
ansible-vault encrypt_string --vault-id @prompt --stdin-name 'encrypted_variable_name'
```
