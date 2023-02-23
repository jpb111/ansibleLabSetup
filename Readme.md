# Ansible lab setup with Ubuntu and CentOS host containers 

Go to http://localhost:7681/ in the browser 
Click ansible terminal and click ubuntu c and login. 

username: ansible 
password: password 


```

update ubuntu 

```bash
sudo apt update

```
## Copy ssh key to the hosts 

```bash

cd Tools 

```
run the below script 

```
./copyPublicSshKey

```
 

```bash

#!/bin/bash

# Description: 
# copy ssh public key to other systems

# Usage: 

# Print text to the screen 

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



```




if there is any the permission issues, change the permission of the script file

```bash

chmod 744 copyPublicSshKey


```




```bash

ansible -i,ubuntu1,ubuntu2,ubuntu3,centos1,centos2,centos3 all -m ping

```


