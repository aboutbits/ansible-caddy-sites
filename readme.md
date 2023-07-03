Ansible Caddy Sites Role
========================

Configure Caddy sites role.

## Role Variables

- `caddy_sites_reverse_proxy`: A list of sites, that should be configured as reverse proxies.
- `caddy_sites_redirect`: A list of sites, that should be configured as redirects.
- `caddy_sites_custom`: A list of sites, that provide a custom configuration.

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
        caddy_sites_custom:
          - domain_name: "test1.example.com"
            config_file: "./test1.example.com.j2"
            compression: true
            tls_dns:
              provider: digitalocean
              config: xxx
          - domain_name: "test2.example.com"
            config_file: "./test2.example.com.j2"
            tls_certificate:
              private_key: private-key-content
              certificate: certificate-content
```


## Versioning

In order to have a verioning in place and working, create leightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag 1.0
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d 2.0
git push origin :refs/tags/2.0
git tag 2.0
git push --tags
```
