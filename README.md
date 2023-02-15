# Role Name

This role installs a prometheus node exporter instance and configures it to expose metrics.
The role is based on this [ansible-node-exporter role](https://github.com/cloudalchemy/ansible-node-exporter).


## Requirements

The role was developed and tested on a machine running Debian.
If you want to secure your installation by using TLS, you need to provide appropriate certificates.


## Role Variables


| Name                                |                               Required/Default                                | Description                                                                                                                                                      |
| ----------------------------------- | :---------------------------------------------------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `node_exporter_version`             |                                   `latest`                                    | The version of node exporter that should be installed. If empty or set to `latest` the variable will be set to the newest release.                               |
| `node_exporter_web_listen_address`  |                                `0.0.0.0:9100`                                 | The IP address the service should bind to.                                                                                                                       |
| `node_exporter_web_telemetry_path`  |                                  `/metrics`                                   | Path where the metrics should be served.                                                                                                                         |
| `node_exporter_textfile_dir`        |                           `/var/lib/node_exporter`                            | Directory for the textfile exporter.                                                                                                                             |
| `node_exporter_tls_server_config`   |                                     `{}`                                      | Config for the TLS feature.                                                                                                                                      |
| `node_exporter_basic_auth_users`    |                                     `{}`                                      | List of users and BCRYPT password hashes for basic auth.                                                                                                         |
| `node_exporter_enabled_collectors`  | `["systemd", {"textfile": {"directory": "{{ node_exporter_textfile_dir}}"}}]` | Collectors that will be enabled and their respective configuration. In addition to the collectors defined here there may be others, that are enabled by default. |
| `node_exporter_disabled_collectors` |                                     `[]`                                      | Collectors that would be enabled by default, but should be disabled.                                                                                             |


## Example

The following example playbook assumes that you cloned this role to `roles/node_exporter`
(i.e. the name of the role is `node_exporter` instead of `ansible_node_exporter`).

```yml
- hosts: monitoring
  roles:
    - role: node_exporter
      node_exporter_tls_server_config:
        cert_file: /etc/certs/example.com.crt
        key_file: /etc/certs/example.com.key
      node_exporter_basic_auth_users:
        example: $2b$10$LqwcCTNLbemzY8/RMuGTFuB0xKL0CcMcLsZRubJCnnDUNWvucjb3K #user example with password example
```


## License

This work is licensed under the [MIT License](./LICENSE).


## Author Information

- [Sven Feyerabend (SF2311)](https://github.com/SF2311) _sven.feyerabend at stuvus.uni-stuttgart.de_
