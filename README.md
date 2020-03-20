# Automated K8s Install

Ansible install scripts for installing kubernetes onto a set of pre "created" nodes.

##Prerequisites

You require the following to run this installation.

- Ansible
- Docker
- 1 Master and minimum 2 worker nodes that you have ssh key access to.

##Steps

Clone this repo and cd into it.

`cd automated-k8s-install`

Replace `<MASTER_IP>` and `<WORKER_IP>` in the hosts file with the values from the nodes you have already provisioned.

Set up a non root user on each of the nodes

`ansible-playbook -i hosts initial.yml`

Install the k8s dependencies on each of the nodes

`ansible-playbook -i hosts kube-dependencies.yml`

Set up the Master node

`ansible-playbook -i hosts master.yml`

Set up the Worker node

`ansible-playbook -i hosts worker.yml`

##Confirm Successful install

SSH into your master node

`ssh ubuntu@<MASTER_IP>`

- Make sure you ssh in using the ubuntu user

Get nodes and you should see your 3 nodes all in the ready state

`kubectl get nodes`

##Known issues

- Currently installs K8s version 1.14, this needs to be updated to version 1.17
- You should ssh into each of your nodes to accept the connection before running the install as ansible can't seem to handle the yes/no question
- Next step is to integrate the script with digital ocean directly to provision the nodes it then uses.