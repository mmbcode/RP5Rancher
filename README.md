Side quest: Install Rancher on Raspberry PI 5 systems running Raspberry PI OS lite 64bit. Task includes:

OS Upgrade
- Set the hostnames based on defined inventory (I used rp5n1, rp5n2, etc.).
- Allow TCP Forwarding by SSH Daemon.
- Update all installed packages and clean up post install.
- Remove any existing Docker packages.
- Disable swap if present.
- Set net.bridge-nf-call-iptables to 1.
- Create the /var/lib/docker.
- Reboot (added but untested).

Docker, Helm, Kubernetes
- Setup Docker, Helm, and Kubernetes Repos ( I need to investigate the warnings on the repo adds).
- Install miscellaneous packages & docker-ce, helm, kubeadm, kubectl, and kubelet.
- Hold updates for  docker-ce, helm, kubeadm, kubectl, kubelet.
- Add user identified in inventory to the docker group.

Rancher
- Download RKE and move to /usr/local/bin/rke.
- Copy pre-existing cluster configuration from ansible server to cluster nodes (Note: the cluster configuration was established by running "rke config --name cluster.yml").
- Add the Rancher Helm repository.
- Execute rke up (Note: this doesn't seem to work). 

To do:
1. Test reboot, using patched.changed as trigger.
2. Investigate the warnings from the key adds for docker/kubernetes repos.
3. Correct SSL certificate issues in my prestaged cluster.yml. Basically I need to learn Rancher better....
4. Variablize the host that is used for the rke up command through the inventory in playbook. 

Stretch:
1. Update playbook to execute "rke config" directly instead of using a prestaged cluster.yml.
2. Setup hugepages, I tried but failed miserably bricking rp5 two times.

References:
https://rke.docs.rancher.com/installation

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

https://docs.docker.com/engine/install/debian/#install-using-the-repository

