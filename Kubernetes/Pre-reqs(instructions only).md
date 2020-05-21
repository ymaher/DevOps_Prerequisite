## Pre-req for Cent Os(for any host)

### Instructions only

- 3 GB or More RAM
- 3 CPU or more
- Full network connectivity among all machines in the cluster
- Disable Swap on all nodes
- Disable SELinux on all nodes (reboot all nodes)
- Install kubeadm, kubelet, kubectl, and Docker on all nodes
  - Start and enable docker and kubelet on all nodes
- Initialize the master node
- Configure Pod network (wave, flannal, calico) network plugin
- Join the worker note to master node
  
