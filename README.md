# CockroachDB Ansible Role

This Ansible role will setup a [CockroachDB](https://github.com/cockroachdb/cockroach)
database cluster. The role installs CockroachDB mostly following the [manual deployment guide](https://www.cockroachlabs.com/docs/stable/deploy-cockroachdb-on-premises.html) and uses / expects proper certificate-based authentication.

## Requirements

This role has only been tested with Debian, but should support Ubuntu, RHEL,
and CentOS.

* Ansible - 2.9+ recommended

## Variables

The following variables are supported. When using this role, set variables
inside the role context. For example:

```yaml
  roles:
  - name: cockroachdb
    vars:
      roach_version: v20.1.2
```

### `roach_cluster_name`

- Set the name of the cluster
  - This is useful for uninitialized clusters
- Default: *roach*

### `roach_version`

- Specify the CockroachDB release version to install
- Default: *v20.1.2*

### `roach_pki_custom_ca`

- When set, the system must be already configured with node certificates and
private keys using a [custom CA](https://www.cockroachlabs.com/docs/v20.1/create-security-certificates-custom-ca.html) approach
- When not set, a simple PKI approach will be used with the role generating a CA and node certificates using [`cockroach cert`](https://www.cockroachlabs.com/docs/v20.1/cockroach-cert.html)
- Default: *false*

### `roach_pki_path`

- Path used by the simply PKI approach only for certificate generation and CA key storage
- Default: */etc/pki/cockroach/*

### `roach_path`

- The path prefix for CockroachDB data
- Default: */var/lib/cockroach/*

### `roach_systemd_directory`

- Base folder for systemd configuration
- Default: */etc/systemd/system*

### `roach_cache`

- Total size in bytes for caches
- Default: *.25*

### `roach_max_sql_memory`

- Maximum memory capacity available to store temporary data for SQL clients
- Default: *.25*

### `roach_init_check_user`

- CockroachDB user to authenticate with to check initialization status
  - This is only useful when using a custom CA
- Default: *root*

### `roach_init_cert_path`

- Path to user certs folder when performing initialization check
  - This is only useful when using a custom CA
- Default: *{{ roach_path }}/certs*
