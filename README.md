# proxmox-ansible-k8s

This project is meant to be used by cloud-init [Ansible module](https://docs.cloud-init.io/en/latest/reference/modules.html#ansible)

### TODOs
- Integrate with a secrets manager (Vault, SSM, etc.) so that the CA.crt and CA.key can be stored safely and then be used by the `k8s_nodes` playbook during execution time. Currently I am using the flag `--discovery-token-unsafe-skip-ca-verification` while joining nodes to the cluster, which is not ideal for production environments.
