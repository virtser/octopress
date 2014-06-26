---
layout: post
title: "Vagrant and Ansible"
date: 2014-06-26 16:08
comments: true
published: true
---

I spend few hours recently to learn about [Vagrant](http://vagrantup.com) and [Ansible](http://www.ansible.com/home) to understand better how these tools work together. I'm really excited of potential hiding behind them. Unfortunately not many developers/companies know these tools and using them. So I wanted to share with you what I learned and hope it will help you to discover a concept called "Infrastrucutre as a code" if you didn't know about it before.

## Vagrant
<img style="float: right" src="http://upload.wikimedia.org/wikipedia/commons/8/87/Vagrant.png" width="100px" hspace="5"/>

Basically Vagrant provides you with functionality to create, provision and configure your own isolated development environment. It can be a single machine or number of machines connected in private network. Depends on your application infrastructure. All it does is creates on your laptop a defined set of virtual machines using (by default) VirtualBox. These machines actually defines your development environment.

Vagrant saves its configuration in _Vagrantfile_ which is stored as part of your projects root. It should be also saved in source control as part of your project as it defines how your environment look like and how to create it from scratch if needed. Click [here](https://github.com/virtser/vagrantansible/blob/master/Vagrantfile) to see how a typical Vagrant file looks like.

_Vagrantfile_ includes:

* Definition of your VMs (which boxes: Linux, Windows, etc...)
* Network settings (port forwarding, private network, etc...)
* Provisioning (how to setup a VM after creation from clean box)
* and more other but less useful stuff...

I won't dive into more details. I hope you got the point and if you want to read more about why using Vagrant and what does it provide, you can go [here](http://docs.vagrantup.com/v2/why-vagrant/index.html).

## Ansible

<img style="float: right" src="http://bundles.kunstmaan.be/uploads/media/52f2178e8b342.png" width="100px" hspace="5"/> Ansible is a lightweight, simpler and easier to on board alternative for widely known Chef and Puppet configuration management tools. Like their big brothers its mission is to allow smart provisioning, deployment and configuration management of servers.

Ansible uses a _hosts_ file to define how your environment look like. You can create groups of identical servers as well. Groups are good to define a set of similar machines for later mass provisioning. Example of such file can be found [here](https://github.com/virtser/vagrantansible/blob/master/Ansible/hosts).

Ansible saves its configuration in YAML files called "playbooks" which actually defines how to provision server or number of servers. Example of such file can be found [here](https://github.com/virtser/vagrantansible/blob/master/Ansible/front.yml).

Same as with Vagrant, you save these YAML files along side with your project, because they define how to build your environment.

You can read more about why using Ansible and what does it provide  [here](http://www.ansible.com/how-ansible-works).

## Vagrant and Ansible integration

Vagrant as part of its configuration knows to call Ansible playbooks to provision the VMs that where created. It also automatically creates a hosts file to define the environment for Ansible and to make sure you will be able to provision the Vagrant machines from your laptop.

I don't know if you heard the term "Infrastructure as a code", but these tools actually does exactly that. Which means that you are writing code to define your infrastructure, saving it as part of source control and that you will be able to re-create it at any given time. Whenever it is in development, testing or production environments. That gives you great power to keep your environment infrastructure consistent, testable and repeatable!

Hope it was useful and made you think about how you should work. :)

I created the following example for you in GitHub if you want to play with it a little: [https://github.com/virtser/vagrantansible](https://github.com/virtser/vagrantansible)