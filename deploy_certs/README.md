# Deploy SSL Certificates

This is an ansible-playbook to deploy SSL certificate to Apache HTTPD and Oracle OHS.

## Usage

```shell
ansible-playbook -i hosts_certs -k deploy_certs.yml
```

## Description

The playbook copy new certificate and reload the webserver.

## Notes

Please review and customize the playbook. It contains hardcoded values.