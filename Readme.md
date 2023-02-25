# Ansible lab setup with Ubuntu and CentOS host containers 

Go to http://localhost:7681/ in the browser and login. 
if planning to install kubernetes skip this section and go to install kubernetes below. 

username: ansible,

password: password 


update ubuntu 

```bash
sudo apt update

```
## Copy ssh key to the hosts 

```bash

cd Tools 

```
run the below script to copy the ssh key and test the ansible ping. 

```
./copyPublicSshKey

```
 

```bash

#!/bin/bash

# Description: 
# copy ssh public key to other systems

# Usage: 

# Print text to the screen 

sudo apt update 

ssh-keygen
sudo apt install sshpass
echo password > password.txt

for user in ansible root; do 
  for os in ubuntu centos; do 
    for instance in 1 2 3; do 
      sshpass -f password.txt ssh-copy-id -o StrictHostKeyChecking=no ${user}@${os}${instance}
    done
  done
done

rm password.txt

ansible all -i inventory.py --list-hosts
ansible all -i inventory.py -m ping 




```

## Install kubernetes 

logout and login as root user 

username: root
password: password 

In the home directory git clone the kubernetes installation repository.  

```bash

git clone https://github.com/jpb111/kubernetes-ansible.git

cd kubernetes-ansible


```
go to tools and run the copyPublicShKey script. 

```bash 
cd tools

./copyPublicShKey

```

Create the kubernetes cluster by running the ansible playbook site.yml 

```bash

cd ~
cd kubernetes-ansible

ansible-playbook site.yml 

```

Copy the KUBECONFIG file 

```bash

export KUBECONFIG=/root/kubernetes-ansible/inventory/artifacts/k0s-kubeconfig.yml

```

```bash


```





