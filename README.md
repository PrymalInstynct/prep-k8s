Prep K8s
=========

Prepares Fedora/Red Hat based systems to become Kubernetes Hosts

Requirements
------------

None

Role Variables
--------------

| Variable | Default | Description |
| -------- | ------- | ----------- |
| dnf_timer_hour | 0 | Hour 0-23 for when you would like to execute the dnf-automation.timer systemd service file |

Dependencies
------------

None

Example Playbook
----------------

```yaml
---
- name: Prepare Kubernetes Hosts
  hosts: kubernetes
  become: true
  roles:
    - { role: prep-k8s }
```
Example Inventory
----------------
The inventory uses host_vars to override the default value for the `dnf_timer_hour` variable

```yaml
---
kubernetes:
  children:
    master:
      hosts:
        k8s-control-prod-0:
          ansible_host: 10.10.1.10
          dnf_timer_hour: 0
        k8s-control-prod-1:
          ansible_host: 10.10.1.11
          dnf_timer_hour: 1
        k8s-control-prod-2:
          ansible_host: 10.10.1.12
          dnf_timer_hour: 2
    worker:
      hosts:
        k8s-worker-prod-3:
          ansible_host: 10.10.1.13
          dnf_timer_hour: 3
        k8s-worker-prod-4:
          ansible_host: 10.10.1.14
          dnf_timer_hour: 4
```

Example Playbook Execution
--------------------------

```
ansible-playbook -i inventory.yml playbook/prep-k8s.yml -K
```

License
-------

MIT

Author Information
------------------

Chad Zimmerman
