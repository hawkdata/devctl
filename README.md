# Developement Environement Control Center

## Control Center

#### Pacakge Repository

#### Inventory

#### Playbook


### Ansible Installation on WSL Ubuntu



## passwordless login

```
    sudo apt install openssh-server
```


```
ssh-keygen -t ed25519
```

This will create two files in your ~/.ssh/ directory: id_ed25519 (your private key) and id_ed25519.pub (your public key).


```
ssh-copy-id user@remote_ip_address
```
You will be prompted to enter the password for the user on the remote server. After successful authentication, ssh-copy-id will add your public key to the ~/.ssh/authorized_keys file on the remote server.

Test Passwordless SSH Login:



##  Ask password when sudo
```
ansible-playbook -i your_inventory --ask-become-pass your.playbook.yaml
```


--- @end
