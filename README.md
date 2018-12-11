Kubernetes local install with kubeadm
======================================

This ansible playbook will install a kubernetes proof of concept environment on centos 7 with kubeadm.

**Please use this playbook not for production environments!** 

version = 1.13.0

## Requirements
* vagrant 
* virtualbox
* ansible 2.7 or higher
* 8gb mem available on your system or decrease worker nodes to 2 or 1
* minimal 2 cpu's for each vm

## Getting started

### Deployment

Generate [ssh-key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

***Spin up vm's***
```bash
$ git clone [git-url]
$ cd kubeadm-ansible
$ vagrant up
```

***Add your public key to vagrant user***
```
$ cat [localtion public key] example: cat ~/.ssh/id_rsa.pub
$ vagrant ssh kubemaster1
$ vi ~/.ssh/authorized_keys
```
Do this also for worker1/2/3


***Run ansible playbook***
```
$ cd ansible
$ ansible-playbook -i inventory/hosts -u vagrant --private-key [location private key] playbook.yml
```

### Usage

```bash
$ vagrant ssh kubemaster1
$ sudo su - kubernetes
$ kubectl get nodes
$ kubectl get pods
```

### Dashboard

Get token to login to dashboard 
```bash
$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```

***Kube-proxy***
```bash
$ kubectl proxy &
```

***ssh tunnel to dashboard***
```
$ ssh -L 8001:127.0.0.1:8001 -i [location private key] vagrant@10.10.43.10
```

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

Reference on [github](https://github.com/kubernetes/dashboard/)

## Tasks

https://kubernetes.io/docs/tasks/


