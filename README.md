pfsense (r) builder
===============

This is a project to build a Vagrant box capable of building pfsense (r) from source.

The long-term goal is automating creation of EC2 pfsense (r) images in the 2.2 series

Invocation
==========

vagrant plugin install vagrant-aws
vagrant plugin install nugrant
vagrant up --provider=aws

Notes
=====

At this time, I am abandoning this work and instead using OPNsense. The current code
state is that it will install some of the preqs necessary to build pfsense (r) on
FreeBSD (r) . Remaining tasks include getting access to the pfsense-tools repo and
mirroring to the Vagrant host, as well as using `fast_cvsup` to bring in FreeBSD (r)
sources.
