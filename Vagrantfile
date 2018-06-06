require 'vagrant-aws'
require 'vagrant-env'

API_VERSION = '2'

Vagrant.configure(API_VERSION) do |config|
  config.env.enable

  config.vm.box = 'aws-dummy'

  config.vm.provider 'aws' do |aws, override|
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']

    aws.keypair_name = 'cv-sandbox'

    aws.ami = 'ami-e251209a'
    aws.region = 'us-west-2'

    aws.instance_type = 't2.micro'
    aws.security_groups = ['SSH From Anywhere']

    aws.tags = {
        'Name' => 'CV TempInstance'
    }

    override.ssh.username = 'ec2-user'
    override.ssh.private_key_path = '~/.ssh/cv-sandbox.pem'
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'playbook.yml'
    ansible.compatibility_mode = '2.0'
  end
end
