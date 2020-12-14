# Kubernetes-kubeadm-install

#Docker-Setup - Master and Worker Node

sudo apt-get update
sudo apt-get install docker.io
docker ––version
sudo systemctl enable docker
sudo systemctl status docker
--------------------------------------------------
#Kubernetes install - Master and Worker Node

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get install kubeadm kubelet kubectl
sudo apt-mark hold kubeadm kubelet kubectl
kubeadm version
sudo hostnamectl set-hostname master-node
sudo hostnamectl set-hostname worker01

#Master Node Only

sudo kubeadm init --pod-network-cidr=10.244.0.0/16
#Once this command finishes, it will display a kubeadm join message at the end. Make a note of the whole entry. This will be used to join the worker nodes to the cluster.
sudo mkdir -p $HOME/.kube 
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl get pods --all-namespaces
#Join Command will be different for each setup
#example - kubeadm join 172.31.47.90:6443 --token wp6z1e.qw4zuv111jkdmq98 \
    --discovery-token-ca-cert-hash sha256:5d21245ca3423ff58602de09cb9d6a13b27ed0c686483051bdbe896de66f0e62
kubectl get nodes



