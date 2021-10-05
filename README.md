# Steps to install rancher k8s
#### Recommended to go with 3 nodes wherein 1master with 2workers.

Step 1: Update /etc/hosts file with number of nodes taken with their IP address
```
Example:
167.254.204.77  master
167.254.204.59  node1
167.254.204.52  node2
```

Step 2: Disable all swap.
```
# swapoff -a 
```

Step 3: Install Docker Runtime Container.

```
Refer URL - https://docs.docker.com/engine/install/centos/
# sudo groupadd docker
# sudo usermod -aG docker centos
```

Step 4: Generate a ssh-keygen  in master and copy it on all nodes.
```
# ssh-keygen
# ssh-agent bash -c "ssh-add key.pem ; ssh-copy-id -i ~/.ssh/id_rsa.pub centos@master" 
# ssh-agent bash -c "ssh-add gcp-pvt.pem ; ssh-copy-id -i ~/.ssh/id_rsa.pub centos@node1"
# ssh-agent bash -c "ssh-add gcp-pvt.pem ; ssh-copy-id -i ~/.ssh/id_rsa.pub centos@node2"
```

Step 5:  Download rancher linux lib file from below URL and move lib file /usr/local/bin.
```
# wget https://github.com/rancher/rke/releases/download/v1.1.16/rke_linux-amd64
# sudo mv rke_linux-amd64 /usr/local/bin/
# cd /usr/local/bin 
# mv rke_linux-amd64 rke
# chmod 0777 rke
# rke --version
```

Step 6: Configure rancher file with node details with below cmd.
```
# rke config
```

Step 7: Start rancher installation with below cmd.
```
# rke up
```

Step 8: Download kubectl and move to .kube/config and permission change.
```
# curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
# sudo cp kubectl /usr/local/bin/
# mkdir .kube
# cp kube_config_cluster.yml .kube/config
# sudo chmod 0777 /usr/local/bin/kubectl
# kubectl get pod -A
```









