pfsense builder
===============

This is a project to build a Vagrant box capable of building pfsense from source.

The long-term goal is automating creation of EC2 pfsense images in the 2.2 series

Invocation
==========

vagrant plugin install vagrant-aws
vagrant plugin install nugrant
vagrant up --provider=aws
