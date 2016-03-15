Ansible Pull
=========

Use `ansible` in push mode to configure a remote machine to run `ansible-pull` as `root` on a schedule.

Requirements
------------

- cron
- logrotate

Role Variables
--------------

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `ansiblepull_workdir` | `/var/lib/ansible/local` | Directory where repository is cloned. |
| `ansiblepull_repo` | `https://github.com/samdoran/` | Remote repository to clone when running `ansible-pull`. |
| `ansiblepull_playbook` | `{{ ansiblepull_workdir }}/site.yml` | Playbook to run with `ansible-pull`. |
| `ansiblepull_logfile` | `/var/log/ansible-pull.log` | Where to log output from `ansible-pull`. Also gets rotated. |
| `ansiblepull_vault_password_file` | `/root/.vault` | File to hold Ansible vault key. **Not recommonded unless you aware of the implications of storing keys in clear text on remote hosts.** |
| `ansiblepull_vault_password` | `SuperSecretKey` | Vault key, in plain text, that will be inserted int `ansiblepull_vault_password_file`. **Not recommonded unless you aware of the implications of storing keys in clear text on remote hosts.** |
| `ansiblepull_ssh_private_key` | [see `defaults/main.yml`] | Optionally define an SSH private key that will be installed for `root` on the remote host. If this is not defined, a new key will be generated and the pubil SSH key will be output at the end of the play. |
| `ansible_known_hosts` | `[]` | List of SSH host keys to add to `/root/.ssh/known_hosts`. |
| `ansiblepull_cron` | [see `defaults/main.yml`] | Cron configuration for job that runs `ansible-pull`. The default settings run `ansible-pull` every ten minutes. |


Dependencies
------------

- samdoran.repo-epel

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Setup Ansible Pull
      hosts: all
      become: True

      roles:
        - samdoran.repo-epel
        - ansible-pull

License
-------

MIT
