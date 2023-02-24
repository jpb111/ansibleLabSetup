# Ansible lab setup with Ubuntu and CentOS host containers 

Go to http://localhost:7681/ in the browser and login

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

In the home directory git clone the kubernetes installation repository.  

```bash

cd ..


git clone https://github.com/jpb111/kubernetes-ansible.git

```

Create the kubernetes cluster by running the ansible playbook site.yml 

```bash

cd kubernetes-ansible

ansible-playbook site.yml 

```







