Ansible Caddy Sites Role
========================

Configure Caddy sites role.

## Role Variables

- `caddy_sites_reverse_proxy`: A list of sites, that should be configured as reverse proxy.

## Example Playbook

```yaml
- hosts: all
  tasks:
    - ansible.builtin.include_role:
        name: ansible-caddy-sites
      vars:
        caddy_sites_reverse_proxy:
          - domain_name: "test1.example.com"
            destination_url: https://example.com
          - domain_name: "test2.example.com"
            destination_url: https://example.com
            compression: true
            headers_up:
              - operation: +
                field: Host
                value: example.com
            tls_dns:
              provider: digitalocean
              config: xxx
        caddy_sites_redirect:
          - domain_name: "test1.example.com"
            destination_url: https://example.com
            tls_dns:
              provider: digitalocean
              config: xxx
          - domain_name: "test2.example.com"
            destination_url: https://example.com
            tls_certificate:
              private_key: private-key-content
              certificate: certificate-content
          - domain_name: "test2.example.com"
            destination_url: https://example.com
            permanent: true
```


## Versioning

In order to have a versioning in place and working, create lightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag v2
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d v2
git push origin :refs/tags/v2
git tag v2
git push --tags
```
