# L7LB
## Layer7 LoadBalancer

This is an ansible-playbook to configure a Red Hat Enterprise Linux 8.x server
as a Layer7 loadbalancer based on [HAProxy](https://www.haproxy.org/), [Keepalived](https://keepalived.org/) and [maint-http](https://github.com/nicolar/maint-http).

## Usage

```shell
ansible-playbook -k --vault-id @prompt -i hosts_l7lb -l webtier_qa l7lb.yaml
```

## Description

The playbook performs several steps:
1. Set RHEL subscriptions
2. Install required RPM packages
3. Enable selinux
4. Configure firewalld to permit intra LoadBalancer servers communication
    - Create a firewalld service called "vrrp"
    - Create a firewalld zone called (again) "vrrp" between the 2 LoadBalancer servers and allows VRRP service there
5. Configure firewalld to accept external http/https connections
6. Configure HAProxy
    - Copy config file
    - Set selinux
    - Set rsyslog
    - Start service
7. Configure Keepalived
    - Copy config file
    - Start service
8. Configure maint-http
    - Create unix user
    - Copy maint-http software
    - Copy HTML resources
    - Copy systemd unit file
    - Start service

## Notes

Please customize keepalived.conf file with your VIPs addresses, customize also haproxy.cfg with your desired settings and backends.

Remember also that a ```rhsm_secrets.yaml``` containing your RH subscription credential is needed.

Here an example:
```yaml
username: myusername@example.com
password: !vault |
        $ANSIBLE_VAULT;1.1;AES256
        <replace with your values>
```

You can generate an encrypted value with the following command:
```shell
ansible-vault encrypt_string --vault-id @prompt --stdin-name 'name_of_password_var'
```