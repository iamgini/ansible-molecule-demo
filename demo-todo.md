- show molecule --version
- show ansible.cfg
- show ansible --version
-

- molecule list

```shell
$  molecule list
INFO     Running default > list
                          ╷             ╷                  ╷               ╷         ╷
  Instance Name           │ Driver Name │ Provisioner Name │ Scenario Name │ Created │ Converged
╶─────────────────────────┼─────────────┼──────────────────┼───────────────┼─────────┼───────────╴
  molecule-ubi8-init-1    │ default     │ ansible          │ default       │ unknown │ false
  molecule-ubi9-init-1    │ default     │ ansible          │ default       │ unknown │ false
  molecule-centos-stream8 │ default     │ ansible          │ default       │ unknown │ false
                          ╵             ╵                  ╵               ╵         ╵
```

- molecule login

```shell
$ molecule login --host molecule-ubi8-init-1
INFO     Running default > login
[root@8320931bbb22 /]#
```

- molecule matrix

```shell
$  molecule matrix destroy
INFO     Test matrix
---
default:
  - dependency
  - cleanup
  - destroy
```

- custom scenarios
  - show by disabling the destroy part - containers wont be deleted.
  - Then show with container cleanup as part of deletion

```yaml
scenario:
  create_sequence:
    - dependency
    - create
    - prepare
  check_sequence:
    - dependency
    - cleanup
    - destroy
    - create
    - prepare
    - converge
    - check
    - destroy
  converge_sequence:
    - dependency
    - create
    - prepare
    - converge
  destroy_sequence:
    - dependency
    - cleanup
    - destroy
  test_sequence:
    - dependency
    - cleanup
    - destroy
    - syntax
    - create
    - prepare
    - converge
    - idempotence
    - side_effect
    - verify
    - cleanup
    - destroy
```