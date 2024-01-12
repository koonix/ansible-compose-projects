# ansible-compose-projects

Ansible roles for running Docker Compose projects.

## Roles

### compose_projects

General-purpose role for running Docker Compose projects.

This role handles removals as well.

| Variable                                                  | Required | Description |
|-----------------------------------------------------------|:--------:|-------------|
| `compose_projects`                                        | ✔        | List of projects to run. |
| `compose_projects[].name`                                 | ✔        | Title of the project. |
| `compose_projects[].compose`                              | ✔        | Map of the docker compose file contents. Default: `{}`. |
| `compose_projects[].assets`                               |          | List of files to create in the project directory, next to the docker compose file. Default: `[]` |
| `compose_projects[].assets[].name`                        | ✔        | Name of the file. |
| `compose_projects[].assets[].content`                     | ✔        | Content of the file. |
| `compose_projects[].assets[].mode`                        |          | Permissions of the file. Default: `'644'` |
| `compose_projects[].assets[].hooks_pre`                   |          | Commands to run before the asset is updated, defined as a list of [`argv`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html#parameter-argv) lists. Commands run in the project directory. Deduplicated across all assets. Default: `[]` |
| `compose_projects[].assets[].hooks_post`                  |          | Commands to run after the asset is updated, defined as a list of [`argv`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html#parameter-argv) lists. Commands run in the project directory. Deduplicated across all assets. Default: `[]` |
| `compose_projects_lib_dir`                                |          | Where to put the project directories. Default: `/var/lib/ansible-compose-projects` |
