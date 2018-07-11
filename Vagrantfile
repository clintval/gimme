require 'vagrant-aws'
require 'vagrant-env'

Vagrant.configure('2') do |config|
  config.env.enable
  config.vm.box = 'aws-dummy'
  config.vm.provider 'aws' do |aws, override|
    aws.ami                    = ENV['AWS_AMI']
    aws.instance_type          = ENV['AWS_INSTANCE_TYPE']
    aws.keypair_name           = ENV['AWS_KEYPAIR_NAME']
    aws.region                 = ENV['AWS_REGION']
    aws.access_key_id          = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key      = ENV['AWS_SECRET_ACCESS_KEY']

    # Open SSH ports for all incoming connections.
    aws.security_groups        = ['SSH From Anywhere']

    # Increase the seconds for high timeout connections.
    aws.instance_ready_timeout = 180  # seconds


    # Do not provision greater than 999Gb until this issue is addressed:
    #
    #     https://github.com/mitchellh/vagrant-aws/issues/547
    #
    aws.block_device_mapping = [
      {
        'DeviceName'              => '/dev/sda1',
        'Ebs.VolumeSize'          => 900,
        'Ebs.VolumeType'          => 'gp2',
        'Ebs.DeleteOnTermination' => true
      }
    ]

    aws.tags = {
        'Name'  => ENV['AWS_INSTANCE_TAG_NAME'],
        'Owner' => ENV['AWS_INSTANCE_TAG_OWNER']
    }

    override.ssh.username         = 'ec2-user'
    override.ssh.private_key_path = ENV['PRIVATE_KEY_PATH']
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'playbook.yml'
    ansible.compatibility_mode = '2.0'
  end
end
