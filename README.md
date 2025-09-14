# Ansible role for installing docker on a host

Features:

- installs latest docker-ce
- installs docker python module
- installs docker-compose
- (optional) installs support for docker buildx multiarchitecture builds
- (optional) performs a docker system prune

## Requirements

Provisioning host:

- ansible 2.15 or later

Host that will run docker

- Ubuntu 22.04 or 24.04

## How to use this role

Add this role to your Ansible playbook file.

```yaml
- name: install docker
  role: xronos_docker_ansible
```

## Variables

- `docker_prune`: prune docker containers, images and networks. Default is `false`.
- `docker_add_ansible_user_to_docker_group`: Add current Ansible user to the docker group. Default is `true`.

### multiarchitecture builds

- `docker_multiarch`: install QEMU. Default is `false`.
- `docker_multiarch_containerd_snapshot`: use containerd-shapshot and create a buildx builder using the `docker-container` driver. Ignored if `docker_multiarch` is false. Defaults is `false`.
- `docker_multiarch_containerd_builder_name`: docker buildx container name for multiarchitecture builds. Used only if `docker_multiarch` and `docker_multiarch_containerd_snapshot` are true. Default is `multiarch`.

### docker authorization

- `docker_auth`: docker authentication token. When present, is written to the user's docker config.json. Default is empty.
- `docker_auth_registry`: doker authentication registry. Default is "https://index.docker.io/v1/". Applies only if `docker_auth` is set.

### Versions

- `docker_version`: version of docker-ce to install. Default is empty (latest).
- `docker_buildx_version`: version of docker-buildx-plugin to install. Default is empty (latest).
- `docker_compose_version`: version of docker-compose-plugin to install. Default is empty (latest).
- `python3_docker_version`: version of python3-docker package to install. Default is empty (latest).
