# vagrant-k8s learn

A very quick one to get kubernetes going on your local vagrant with 3 nodes.\
I've been messing too much with my own setup, so having a quick build is just nice to have.

As presented in A Cloud Guru CKA lesson Chapter 2.3 "Building a Kubernetes Cluster" https://acloudguru.com/course/certified-kubernetes-administrator-cka

# Stuff used

ubuntu 20.10\
vagrant 2.2.9\
virtualbox 6.1.16\
ansible 2.9.9

# Notes
Adjust `Vagrantfile` to suit your VMs needs (cpu, ram and what not)

k8s version here is `1.20.1-00`. Change in `roles/k8s-install/defaults/main.yaml` to what you need.

Add `127.0.0.1 kubernetes.default` to `/etc/hosts` on your host if you wish to talk to the cluster from outside of `control` node.

Uncomment last part in `Vagrantfile` if you want to have full-auto install with just `vagrant up`

#Usage
```
vagrant up && ansible-playbook site.yaml
```



