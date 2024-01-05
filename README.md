# ansible-docker-compose

Ansible roles for configuring and running Docker Compose stacks.

## Roles

### docker_compose

General-purpose role for configuring and running Docker Compose stacks.

This role handles instance removals as well.

| Variable                                                  | Required | Description |
|-----------------------------------------------------------|:--------:|-------------|
| `docker_compose_instances`                                | ✔        | List of instances to run. |
| `docker_compose_instances[].name`                         | ✔        | Title of the instance. |
| `docker_compose_instances[].compose`                      | ✔        | Map of extra configs to append to docker compose. Default: `{}`. |
| `docker_compose_instances[].assets`                       |          | List of files to create in the instance directory, next to the docker compose file. Default: `[]` |
| `docker_compose_instances[].assets[].name`                | ✔        | Name of the file. |
| `docker_compose_instances[].assets[].content`             | ✔        | Content of the file. |
| `docker_compose_instances[].assets[].mode`                |          | Permissions of the file. Default: `'644'` |
| `docker_compose_instances[].compose_project_name`         |          | Name of the docker compose project. Defaults to the value of `docker_compose_instances[].name`. |
| `docker_compose_instances[].compose_version`              |          | Version of the docker compose file. Default: `'3.8'` |
| `docker_compose_lib_dir`                                  |          | Where to put docker files, configs, etc. Default: `/var/lib/ansible-docker-compose` |
