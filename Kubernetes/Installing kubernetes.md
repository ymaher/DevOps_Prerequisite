## Installing kubernetes 

### Steps to follow
1. Create master and nodes and be a root user for all nodes
 
 > `$ sudo su - `
 
2. Disable Firewall | Swap on all nodes
 
 > `$ systemctl stop firewalld`
 
 > `$ systemctl disable firewalld`
  
 > `$ swapoff -a`
 
 > `$ sed -i.bak -r 's/(.+ swap .+)/#\1/' /etc/fstab`
 
3. Disable SeLinux on all nodes (for temp 1st Line)
  
 > `$ setenforce 0` for temporary
 
 > `$ sed -i 's/enforcing/disabled/g' /etc/selinux/config`
 
4. Reboot all nodes
 
 > `$ yum update -y`
 
5. Add kubernetes repo (master and worker nodes)
 
 ```
 cat <<EOF > etc/yum.repos.d/kubernetes.repo
 [kubernetes]
 name=Kubernetes
 baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
 enabled=1
 gpgcheck=1
 repo_gpgcheck=1
 gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
 exclude=kube*
 EOF
 ```
 
6. Install Docker (master and worker nodes)
 
 > `$ yum update -y`
 
 > `$ yum install -y docker`
 
7. Start and enable the services of docker (master and worker nodes)
 
 > `$ systemctl start docker && $ systemctl enable docker `
 
8. Install kubelet, kubeadm, kubectl and start kubelet (master and worker nodes)
 
 > `$ yum install -y kubeadm kubelet kubectl --disableexcludes=kubernetes`
 
 > `$ systemctl enable kubelet && systemctl start kubelet`
 
9. This is for fixing issue where traffic being routed to incorrect due to ip tables being by pass (ip forward to enable)
  ```
  cat <<EOF > /etc/sysctl.d/k8s.conf
  net.bridge.bridge-nf-call-ip6tables = 1
  net.bridge.bridge-nf-call-iptables = 1
  EOF
  
  sysctl net.bridge.bridge-nf-call-iptables=1
  sysctl net.ipv4.ip_forward=1
  sysctl --system
  echo "1" > /proc/sys/net/ipv4/ip_forward
  ```
  Restart the systemd demon and kubelet services
 
 > `$ systemctl daemon-reload`
 
 > `$ systemctl restart kubelet`

 
10. Only on (master node)
 
 > `$ kubeadm init --pod-network-cidr=10.240.0.0/16`
 
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

17. On Master Node ()
> `$ kubectl get no`

18. We can try run sample application to run and check if this is working
> `$ kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port:8080 `

19: We can check the pods which are deployed as a part of deployment
> `$ kubectl get po`


https://gist.github.com/rkaramandi/44c7cea91501e735ea99e356e9ae7883
