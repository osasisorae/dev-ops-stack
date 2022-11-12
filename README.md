# didactic-octo-memory

Simple devops project to strenghten the following tools

###Tools:
Vagrant , Ansible, Docker, Docker Swarn.

### Goals:
- Provide multiple linux servers using vagrant.
- Run a playbook that automates the configuration of the above servers
- Containerize an enterprise web application
- Convert the servers to docker swarm nodes and bring up the application on the swarm


### Guide Ubuntu 20.04
#### Install vagrant
```
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install vagrant
```

#### Install hypervysor providers(Oracle Virtual-Box)
Note: We could choose VMware, Docker, Hyper-V, [Virtual-Box](https://www.virtualbox.org/wiki/Linux_Downloads), or a custom Provider.

### Start
```
vagrant up
vagrant ssh control
```
[vm](./assets/vagrant_up.png)

#### Create ssh key and push out to servers
```
ssh vagrant@node1 #ssh should be installed by default
ssh-keygen
ssh-copy-id node1
ssh-copy-id node2
ssh-copy-id node3

# test ssh access
ssh vagrant@node2
```
## Install ansible playbook 
```
mkdir ansible
cd ansible
touch myhost
touch playbook1.yml
# download the content of these files from the website

vagrant ssh control
sudo apt update
sudo apt upgrade -y
sudo apt install ansible
cd /vagrant/ansible/
ansible nodes -i myhost -m command -a hostname # test

```
### Run ansible playbook to install docker
```ansible-playbook -i myhost -K playbook1.yml```

### test docker is installed on node2
```
ssh vagrant@node2
docker run hello-world

```
### Run flask app using docker compose
```
# go back to root directory
mkdir docker
touch app.py && touch docker-compose.yml \
&& touch Dockerfile && touch requirements.txt
# download the content of these files from the website

vagrant ssh control
ssh vagrant@node2
cd /vagrant/docker/
docker-compose up

# open a new server in a new terminal and test port 5000
vagrant ssh control
curl node2:500
```

### Container orchestration with docker swarn
```

```
