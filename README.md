# proxmox-ansible-k8s

This project is meant to be used by cloud-init [Ansible module](https://docs.cloud-init.io/en/latest/reference/modules.html#ansible)

## Stack
- Provisions a k8s control-plane containing Containerd (CRI), Flannel (CNI), MetalLB (Load Balancer) and nginx-ingress (Ingress controller).
- Provisions k8s nodes containing Containerd (CRI)
- Provisions OpenVPN for worker nodes that needs VPN.

### TODOs
- Integrate with a secrets manager (Vault, SSM, etc.) so that the CA.crt and CA.key can be stored safely and then be used by the `k8s_nodes` playbook during execution time. Currently I am using the flag `--discovery-token-unsafe-skip-ca-verification` while joining nodes to the cluster, which is not ideal for production environments.
- Use a secrets manager to provide the VPN configuration and secret.
- Find a way to label the k8s VPN worker node to include the label `vpn=true`. It needs to be done on the control-plane but since Terraform spins up the control-plane first, couldn find a good way to do it on the current approach. Currently it needs to be done manually after the cluster is completely up. Maybe a solution is to have an Ansible controller to execute these tasks, instead of the playbooks being executed inside the hosts.
