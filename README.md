# ansible-compose-projects

Ansible roles for running Docker Compose projects.

## Roles

### compose_projects

General-purpose role for running Docker Compose projects.

This role handles removals as well.

Requires Docker and it's Compose plugin to be installed.
[https://github.com/koonix/ansible-docker](Shameless plug).

| Variable                                                  | Required | Description |
|-----------------------------------------------------------|:--------:|-------------|
| `compose_projects`                                        | ✔        | List of projects to run. |
| `compose_projects[].name`                                 | ✔        | Title of the project. |
| `compose_projects[].compose`                              | ✔        | Map of the docker compose file contents. Default: `{}`. |
| `compose_projects[].pre_start`                            |          | Commands to run before any of the containers in the project are (re)started. See the Hooks section below. Default: `[]` |
| `compose_projects[].post_start`                           |          | Commands to run after any of the containers in the project are (re)started. See the Hooks section below. Default: `[]` |
| `compose_projects[].assets`                               |          | List of files to copy to the project directory, next to the docker compose file. Default: `[]` |
| `compose_projects[].assets[].type`                        |          | Can be `file` or `template` to indicate the type of the asset. |
| `compose_projects[].assets[].src`                         |          | Local path to the file or template. `assets[].content` takes effect if not provided and `assets[].type` is `file`. |
| `compose_projects[].assets[].content`                     |          | Content of the file. Works only when `assets[].type` is `file`. `assets[].src` takes effect if not provided. |
| `compose_projects[].assets[].dest`                        |          | Name of the file in the destination. Defaults to the basename of `assets[].src`. |
| `compose_projects[].assets[].mode`                        |          | Permissions of the file. Default: `'644'` |
| `compose_projects[].assets[].no_log`                      |          | Whether to enable [`no_log`](https://docs.ansible.com/ansible/latest/reference_appendices/logging.html#protecting-sensitive-data-with-no-log) for the installation of this item. Default: `false` |
| `compose_projects[].assets[].pre_update`                  |          | Commands to run before the asset is updated. See the Hooks section below. Default: `[]` |
| `compose_projects[].assets[].post_update`                 |          | Commands to run after the asset is updated. See the Hooks section below. Default: `[]` |
| `compose_projects_lib_dir`                                |          | Where to put the project directories. Default: `/var/lib/ansible-compose-projects` |
| `compose_projects_no_log_include`                         |          | Whether to enable [`no_log`](https://docs.ansible.com/ansible/latest/reference_appendices/logging.html#protecting-sensitive-data-with-no-log) when including tasks, to prevent cluttering ansible's CLI output. Default: `true` |

#### Hooks

Pre-update hooks of all assets
are deduplicated and called one after another *before* any asset is installed.

Similarly, post-update hooks of all assets
are deduplicated and called one after another *after* all assets are installed.

Hooks are executed with the project directory as their working directory.

The value of each hook should be a list.

In `pre_start` and `post_start`,
Each item of the list should be an [`argv` list](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html#parameter-argv).

In `assets[].pre_update` and `assets[].post_update`,
Each item of the list should be either an [`argv` list](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html#parameter-argv),
or one of the following special strings:

| String               | Equivelant command |
|----------------------|--------------------|
| `stop`               | `docker compose stop` |
| `down`               | `docker compose down` |
| `build`              | `docker compose build` |

For example:

```yaml
  post_update:
    - build
    - [ echo, hello, world ]
```

#### Usage

Example [requirements.yml](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-roles-and-collections-from-the-same-requirements-yml-file]) file:

```yaml
collections:
  - name: https://github.com/koonix/ansible-compose-projects
    type: git
    version: 0.2.3
```

Example usage in a playbook:

```yaml
- name: Roles
  hosts: all
  roles:
    - koonix.compose_projects.compose_projects
    - ...
```
