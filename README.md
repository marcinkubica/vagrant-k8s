# vagrant-k8s learn
***

A very quick bodge done to get kubernetes going on vagrant with 3 nodes.\
I've been messing too much with my own setup, so having a quick build is just nice to have.

(Mostly) as presented in A Cloud Guru CKA lesson Chapter 2.3 "Building a Kubernetes Cluster" https://acloudguru.com/course/certified-kubernetes-administrator-cka

## Usage
```
vagrant up && ./vagrant-k8s.sh
```
Uncomment last part in `Vagrantfile` if you want to have full-auto install with just `vagrant up`


## Stuff used

ubuntu 20.10 (my host OS)\
vagrant 2.2.9\
virtualbox 6.1.16\
ansible 2.9.9 \
ubuntu 20.4 LTS Focal (guest OS)


## Notes

#### k8s version
Kubernetes version here is `1.20.1-00`. Reason being is in the course there's a section explaining how to upgrade k8s cluster, hence latest version isnt't expected.
Change in `roles/k8s-install/defaults/main.yaml` to what you need.

#### external access
Add `127.0.0.1 kubernetes.default` to `/etc/hosts` on your host if you wish to talk to the cluster from outside of `control` node.
Typically though this would have been achieved by another interface and EXTERNAL-IP config in your k8s

#### vagrant
INTERNAL-IP for workers is based on `enp0s8` network device as presented on my version of virtualbox.
Adjust `internal_ipv4` variable in `hosts.yaml` if your setup is different.


