# Ansible


*** Installation Ansible

*** NEEDED TWO MACHINE
- Ansible control machine
- Ansible host machine (node)

*** Configuring the Ansible Control Node

/// Go to terminal
$ sudo apt update
$ sudo apt install -y ansible
$ ansible --version

/// Install package manager for python
$ sudo apt install python-pip -y 	

/// Setting up an SSH Key pair
$ ssh-keygen
enter
y
enter
$ ls -l ~/.ssh/
$ cat ~/.ssh/id_rsa.pub
copy the key

*** Configuring an Ansible Host

/// Go to terminal
$ sudo apt update
$ sudo apt install openssh-server -y   [install OpenSSH server using]
$ sudo systemctl status sshd
$ sudo systemctl start sshd
$ sudo ufw allow ssh
$ mkdir ~/.ssh
$ touch ~/.ssh/authorized_keys
$ vim ~/.ssh/authorized_keys
paste
:wq

/// The next step is to add an ansible user and then allow password-less access. 
$ sudo adduser ansible
enter   [skip]
enter
enter
enter
enter
y

/// To configure the password-less sudo access type the following in the terminal window for your ansible user:
$ echo "ansible ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ansible
$ hostname -I
copy IP


*** Go to Ansible Control Node

$ ssh-copy-id ansible@10.0.2.15
yes
$ sudo usermod -L ansible    [To disable password-based login use the command]
$ ssh ansible@10.0.2.15

*** Here we are able to access the Ansible host without any password and it is ready for automation.

*** Testing Ansible

/// Setting up the Host Inventory File
$ sudo nano /etc/ansible/hosts   
[-add the below at the start of the file-]

[test-server]
10.0.2.15


/// After you’ve set up the inventory file, you can always check it again by using:
$ ansible-inventory --list -y


*** Testing the Connection

$ ansible all -m ping
[Success] {it means that SSH connection is established between control machine and node machine}
$ ansible all -m ping -u root

*** Ansible will access AWS resource using boto SDK
$ sudo pip install boto boto3
$ sudo apt-get install python-boto -y
$ pip list boto | grep boto


*** Uninstallation of Ansible
$ sudo apt remove ansible
y
