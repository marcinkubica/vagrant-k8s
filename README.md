# vagrant-k8s learn
***

A very quick bodge done to get kubernetes going on vagrant with 3 nodes.\
I've been messing too much with my own setup, so having a quick build is just nice to have.

The setup is basically identical to a certified kubeadm install for bare-metal infrastucture.

## Usage
Full auto provisioning and deployment with
```
vagrant up 
```
Comment out last section in `Vagrantfile` if you don't need full auto.

#### Kick deployment again
`./vagrant-k8s.sh` or `ansible-playbook k8s.yaml`


## Stuff used

* intel osx 12.3.1 monterey (my host OS) - should easily run on your linux laptop
* vagrant 2.2.19
* virtualbox 6.1.32
* ansible 2.12.4
* ubuntu 20.4 LTS Focal (guest OS) - test with ubuntu 22.04 failed for k8s (reason unknown as of yet)


## Notes

#### k8s version
Kubernetes version here is `1.23.5-00`. Reason being is to allow you to learn how to upgrade k8s with kubeadm.
Change in `roles/k8s-install/defaults/main.yaml` to what you need.

#### external access
Add `127.0.0.1 kubernetes.default` to `/etc/hosts` on your host if you wish to talk to the cluster from outside of `control` node.
Typically though this would have been achieved by another interface and EXTERNAL-IP config in your k8s

#### classic vagrant k8s install pitfalls on githubs
Typically in vagrant installs you will endup with worker's internal IPs being `10.0.2.15` This will cause inability to run `kubectl exec`. I've fixed this as below:

#### networking
1. INTERNAL-IP for workers are based on `enp0s8` network device as present on my version of virtualbox.
Adjust `internal_ipv4` variable in `hosts.yaml` if your setup is different. It should not be needed, really.

2. Virtualbox on mac by default might not allow you to create required interfaces.\
   Try creating a following file `/etc//etc/vbox/networks.conf`
   ```
   * 10.0.0.0/8 192.168.0.0/16
   ```
#### various goodies for k8s - service meshes, ingresses, loadbalancers &whatnot
You have a great chance to try them for yourself here. Otherwise try distros like microk8s.

### Estimated build time
6-9 minutes on linux i7-3930K and fairly slowish SSD and 50Mbit internet (and somehow faster on a i9 mac)

### Known issues
`vagrant up --no-provision` will be ignored and ansible will still execute (and should fail safely)

