# Cloud-Init Test

While working with [Raspberry PI Ubuntu images] to build my local [Kubernetes] cluster, I found out that [cloud-init] is the key bootstrap igredient.
Seems that the tool to try all different configurations is [Vagrant].

# Links

This repo contains information from multiple sources which are noted here for now:

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/
https://www.grzegorowski.com/how-to-test-cloud-init-locally-with-vagrant
https://github.com/gosuri/vagrant-env
https://opensource.com/article/20/6/kubernetes-raspberry-pi
https://cloudinit.readthedocs.io/en/latest/topics/examples.html
https://stackoverflow.com/questions/58248190/how-to-use-cloud-init-with-a-debian-based-image-on-google-cloud
https://ostechnix.com/how-to-increase-memory-and-cpu-on-vagrant-machine/
https://stackoverflow.com/questions/23888381/how-to-run-several-boxes-with-vagrant
https://www.vagrantup.com/docs/multi-machine
https://www.vagrantup.com/docs/networking
https://gist.github.com/danielepolencic/ef4ddb763fd9a18bf2f1eaaa2e337544
https://github.com/flannel-io/flannel#flannel
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
https://helm.sh/docs/intro/quickstart/
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
https://stackoverflow.com/questions/47845739/configuring-flannel-to-use-a-non-default-interface-in-kubernetes
https://github.com/flannel-io/flannel/blob/master/Documentation/troubleshooting.md#vagrant
https://rancher.com/blog/2019/2019-03-21-comparing-kubernetes-cni-providers-flannel-calico-canal-and-weave/
https://github.com/bryansullins/vagrantk8scentos
https://docs.projectcalico.org/master/manifests/calico.yaml
https://github.com/vmware-tanzu/sonobuoy
https://www.toptal.com/developers/gitignore/api/vagrant
https://www.apache.org/licenses/LICENSE-2.0.txt

[Raspberry PI Ubuntu images]: https://ubuntu.com/download/raspberry-pi
[Kubernetes]: https://kubernetes.io/
[cloud-init]: https://cloud-init.io/
[Vagrant]: https://www.vagrantup.com/
