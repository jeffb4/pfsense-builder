# -*- mode: ruby; -*-

Vagrant.configure('2') do |config|
  # FreeBSD 10.1 Vagrant "box" (defines aws as the provider, gives a default AMI)
  config.vm.box_url = 'https://github.com/jeffb4/pfsense-builder/raw/master/boxes/freebsd-10.1-aws.box'
  config.vm.box = 'freebsd-10.1-aws'

  # Use NFS as a shared folder
  config.vm.synced_folder ".", "/vagrant", type: 'rsync'

  # Use a real ssh private key for connection
  config.ssh.private_key_path = [ './.vagrantkey', '~/.ssh/identity']
  # Use ec2-user for login
  config.ssh.username = 'ec2-user'
  # Use sh for shell (bash unavailable by default on FreeBSD)
  config.ssh.shell = 'sh'

  config.vm.provider :aws do |aws, override|
    # Most configuration info is pulled from
    # .vagrantuser, handled by nugrant
    aws.access_key_id = config.user.aws.access_key
    aws.keypair_name = config.user.aws.keypair_name
    aws.region = 'us-east-1'
    aws.secret_access_key = config.user.aws.secret_key
    aws.security_groups = config.user.aws.security_groups
    aws.subnet_id = config.user.aws.subnet_id
    aws.tags = { 'Name' => 'pfsense-builder' }
    # install sudo via userdata, otherwise Ansible won't work
    aws.user_data = "#!/bin/sh\nenv ASSUME_ALWAYS_YES=YES pkg bootstrap\npkg install -y sudo\necho '%wheel ALL=(ALL) NOPASSWD: ALL'>/usr/local/etc/sudoers.d/wheel"
  end

  config.vm.provision 'shell', inline: 'sudo pkg install -y python'

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'playbook.yml'
  end
end
