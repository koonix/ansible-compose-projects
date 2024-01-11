# ansible-compose-projects

Ansible roles for running Docker Compose projects.

## Roles

### compose_projects

General-purpose role for running Docker Compose projects.

This role handles removals as well.

| Variable                                                  | Required | Description |
|-----------------------------------------------------------|:--------:|-------------|
| `compose_projects`                                        | ✔        | List of instances to run. |
| `compose_projects[].name`                                 | ✔        | Title of the instance. |
| `compose_projects[].compose`                              | ✔        | Map of the docker compose file contents. Default: `{}`. |
| `compose_projects[].assets`                               |          | List of files to create in the project directory, next to the docker compose file. Default: `[]` |
| `compose_projects[].assets[].name`                        | ✔        | Name of the file. |
| `compose_projects[].assets[].content`                     | ✔        | Content of the file. |
| `compose_projects[].assets[].mode`                        |          | Permissions of the file. Default: `'644'` |
| `compose_projects_lib_dir`                                |          | Where to put docker files, configs, etc. Default: `/var/lib/ansible-compose-projects` |
