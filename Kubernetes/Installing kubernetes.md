## Installing kubernetes 

### Steps to follow
 1. Create master and nodes
 
 2. Disable Swap on all nodes
  
 > `$ swapoff -a`
 
 3. Disable SeLinux on all nodes (for temp 1st Line)
  
 > `$ setenforce 0` for temporary
 
 > `$ sed -i 's/enforcing/disabled/g' /etc/selinux/config`
 
 > `$ grep disabled /etc/selinux/config | grep -v '#' `
 
 4. Reboot all nodes
 
 5. Install Docker on master and worker nodes
 
 > `$ yum update -y`
 
 > `$ yum install -y docker`
 
 6. Start and enable the services of docker
 
 > `$ systemctl start docker `
 
 > `$ systemctl enable docker `
 
 7. Add kubernetes repo
 
 > `$ cat <<EOF > etc/yum.repos.d/kubernetes.repo`
 
 8. Install kubelet, kubeadm, kubectl and start kubelet
 
 > `$ yum install -y kubeadm kubelet kubectl --disableexcludes=kubernetes`
 
 > `$ systemctl enable kubelet && systemctl start kubelet`
 
 9. This is for fixing issue where traffic being routed to incorrect due to ip tables being by pass
  ```
  cat <<EOF > /etc/sysctl.d/k8s.conf
  net.bridge.bridge-nf-call-ip6tables = 1
  net.bridge.bridge-nf-call-iptables = 1
  EOF
  
  sysctl --system
 ```
 
 10. Only on (master node)
 
 >`$ kubeadm init --pod-network-cidr=10.240.0.0/16`
 
 11. We need to run few command as local user as will be mentioned on the screen
 
 12. Copy the kubeadm join command and keep it safe for future use to join new nodes
 
 
13. Configuring pod network on Master node
 
 > `$ kubectl apply -f \ https://raw.githubusercontent.com/coreos/flannel/v0.9.1/Documentation/kube-flannel.yml`
 
14. To check if Pod network in intsalled, we can do it by
 
 > `$ kubectl get pods --all-namespaces`
 
15. Only in (worker node)
 
 > `$ "kubeadm join token" cmd which you have copied from master node wile init`
 
16. To create new token (~not recommended~)

> `$ kubeadm token create --print-join-command`
