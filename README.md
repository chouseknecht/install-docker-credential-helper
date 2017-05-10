# Install Docker credential helper 

An Ansible role to install the appropriate helper for the host operating system.


Performs the following tasks:

- Finds the latest release for [docker-credential-helpers](https://github.com/docker/docker-credential-helpers)
- Identifies and downloads the release file matching the host operating system
- Unarchives the binary, and places it in `/usr/local/bin`

Tested platforms

- Debian
- Red Hat
- OSX

## Prerequisites 

- sudo access is required for copying the binary to `/usr/local/bin` 
- [Ansible 2.0+](https://github.com/ansible/ansible)

## Defaults

**docker_repo:**  docker/docker-credential-helpers

> Docker repo name

**docker_github_url:** https://api.github.com/repos

> GitHub API endpoint   

**docker_release_tag_name:** ""

> Only supply a value, if you want a specific release installed. Otherwise, the latest is installed.

**docker_bin_dest:** /usr/local/bin  

> Path where new binary will be installed

## Example Playbook

Below is a sample playbook that includes all of the default parameters. You'll find this exact example in [credential-helper.yml](./credential-helper.yml):

```yaml
---
- name: Install docker credential helper 
  hosts: localhost
  connection: local
  gather_facts: yes
  roles:
    - role: chouseknecht.install-docker-credential-helper
      docker_repo: docker/docker-credential-helpers
      docker_github_url: https://api.github.com/repos
      docker_release_tag_name: ""
      docker_bin_dest: /usr/local/bin  
```

After installing the role, copy *credential-helper.yml* to your project directory, and execute it with the `--ask-sudo-pass` option. For example:

```
# Install the role 
$ ansible-galaxy install chouseknecht.docker-credential-helper

# Copy the playbook from your roles path to the current working directory 
$ cp ${ANSIBLE_ROLES_PATH}/chouseknecht.docker-credential-helper/credential-helper.yml .

# Create a localhost inventory file
$ echo "localhost">./inventory

# Run the playbook
$ ansible-playbook -i inventory --ask-sudo-pass credential-helper.yml
```

## Dependencies

None

## License

Apache v2

## Author 

[@chouseknecht](https://github.com/chouseknecht)
