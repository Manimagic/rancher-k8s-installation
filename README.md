# Steps to install rancher k8s

Step 1: Generate a ssh-keygen in master and copy it on all nodes.
```
# ssh-keygen
# ssh-agent bash -c "ssh-add key.pem ; ssh-copy-id -i ~/.ssh/id_rsa.pub centos@master" 
# ssh-agent bash -c "ssh-add gcp-pvt.pem ; ssh-copy-id -i ~/.ssh/id_rsa.pub centos@node1"
```

Step 2: Disable all swap.
```
# swapoff -a 
```

Step 3: Install Docker Runtime Container.

```
# sudo yum install -y yum-utils
# sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
# sudo yum install docker-ce docker-ce-cli containerd.io
# sudo systemctl start docker
# sudo usermod -aG docker centos
```

Step 4:  Download rancher linux lib file from below URL and move lib file /usr/local/bin.
```
# wget https://github.com/rancher/rke/releases/download/v1.3.2/rke_linux-amd64
# sudo mv rke_linux-amd64 /usr/local/bin/
# cd /usr/local/bin 
# mv rke_linux-amd64 rke
# chmod 0777 rke
# rke --version
```

Step 5: Configure rancher cluster.yml file with node details with below cmd.
```
# rke config
```

Step 6: Start rancher installation with below cmd.
```
# rke up
```

Step 7: Download kubectl and move to .kube/config and permission change.
```
# curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
# sudo cp kubectl /usr/local/bin/
# mkdir .kube
# cp kube_config_cluster.yml .kube/config
# sudo chmod 0777 /usr/local/bin/kubectl
# kubectl get pod -A
```
