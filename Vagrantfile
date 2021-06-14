Vagrant.configure("2") do |config|
  config.env.enable # enable .env support plugin (it will let us easily enable cloud_init support)

  # Give a custom name for a VM created by this script for a Vagrant CLI
  # config.vm.define "focal-server-cloudimg-amd64-vagrant"

  # Name for the box image downloaded from the box_url
  # it will be used to create a folder inside ~/.vagrant.d/boxes to avoid re-downloading
  config.vm.box = "focal-server-cloudimg-amd64-vagrant"

  # URL used as a source for the vm.box defined above
  config.vm.box_url = "https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64-vagrant.box"

  config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.cpus = 2
  end

  config.vm.define :master do |master|
    master.vm.box = "focal-server-cloudimg-amd64-vagrant"
    master.vm.hostname = "master"
    master.vm.network :private_network, ip: "10.0.0.10"
    master.vm.provision :shell, privileged: false, inline: $provision_master_node
  end

  # %w{worker1 worker2}.each_with_index do |name, i|
  %w{worker1}.each_with_index do |name, i|
    config.vm.define name do |worker|
    worker.vm.box = "focal-server-cloudimg-amd64-vagrant"
    worker.vm.hostname = name
    worker.vm.network :private_network, ip: "10.0.0.#{i + 11}"
    worker.vm.provision :shell, privileged: false, inline: <<-SHELL
sudo /vagrant/join.sh
echo 'Environment="KUBELET_EXTRA_ARGS=--node-ip=10.0.0.#{i + 11}"' | sudo tee -a /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
sudo systemctl daemon-reload
sudo systemctl restart kubelet
SHELL
    end
  end

  # cloud-init script
  config.vm.cloud_init do |cloud_init|
    # With Ubuntu cloud images you have to use cloud_init to get an access
    cloud_init.content_type = "text/cloud-config"
    cloud_init.path = "cloud-init-test.yml"
  end
end

$provision_master_node = <<-SHELL
OUTPUT_FILE=/vagrant/join.sh
rm -rf $OUTPUT_FILE

# Start cluster
sudo kubeadm init --apiserver-advertise-address=10.0.0.10 --pod-network-cidr=192.168.0.0/16

# Configure kubectl
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl create -f https://docs.projectcalico.org/master/manifests/calico.yaml

kubeadm token create --print-join-command > ${OUTPUT_FILE}
chmod +x $OUTPUT_FILE

# Fix kubelet IP
echo 'Environment="KUBELET_EXTRA_ARGS=--node-ip=10.0.0.10"' | sudo tee -a /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

# Configure flannel
# kubectl create -f /vagrant/kube-flannel1.yml

# curl -o kube-flannel.yml https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
# sed -i.bak 's|"/opt/bin/flanneld",|"/opt/bin/flanneld", "--iface=enp0s8",|' kube-flannel.yml
# kubectl apply -f kube-flannel.yml

sudo systemctl daemon-reload
sudo systemctl restart kubelet
SHELL
