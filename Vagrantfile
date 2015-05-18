# -*- mode: ruby; -*-

Vagrant.configure('2') do |config|
  config.vm.box_url = 'https://github.com/jeffb4/pfsense-builder/raw/master/boxes/freebsd-10.1-aws.box'
  config.vm.box = 'freebsd-10.1-aws'

  # Use NFS as a shared folder
  config.vm.synced_folder ".", "/vagrant", type: 'rsync'

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = config.user.aws.access_key
    aws.secret_access_key = config.user.aws.secret_key
    aws.region = 'us-east-1'
  end
end
