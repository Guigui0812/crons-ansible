Cron Role
==========

This Ansible role configures cron jobs on a target host. It allows you to define custom cron jobs using a list of dictionaries with job parameters. The role will iterate over each item and set up the cron job accordingly.

Requirements
------------

- [Ansible](https://docs.ansible.com/) - Ansible must be installed to execute the playbook.

Role Variables
--------------

The following variables are used in this role and can be customized as needed:

| Variable              | Description                                                | Default Value          |
|-----------------------|------------------------------------------------------------|------------------------|
| `host_crons`           | A list of dictionaries defining the cron jobs. Each item contains the following keys: `name`, `minute`, `hour`, `weekday`, `month`, `day`, `job`, and `user`. | `[]` (empty by default) |

Dependencies
------------

This role has no external dependencies.

Example Playbook
----------------

Here is an example of how to use this role in a playbook:

```yaml
- hosts: servers
  become: yes
  roles:
    - role: cron
      host_crons:
        - name: "backup_job"
          minute: "0"
          hour: "3"
          weekday: "*"
          month: "*"
          day: "*"
          job: "/usr/local/bin/backup.sh"
          user: "root"
        - name: "system_cleanup"
          minute: "15"
          hour: "4"
          weekday: "1"
          month: "*"
          day: "*"
          job: "/usr/local/bin/cleanup.sh"
          user: "root"
```

In this example, cron jobs are set up to run a backup script at 3 AM every day, and a system cleanup every Monday at 4:15 AM.

License
-------

BSD