#### Dependencies

- Vagrant
- Ansible
- `aws-cli`

#### Vagrant Plugins

```bash
❯ vagrant plugin install vagrant-env
❯ vagrant plugin install vagrant-aws
```

#### Vagrant Box

A dummy box is provided for the `aws` provider. This acts as a pass-through for Vagrant.

```bash
❯ address=https://github.com/clintval/gimme/raw/master/example-box/aws-dummy.box
❯ vagrant box add aws-dummy "${address}" --provider aws
```

## Environment

Load the following variables into your environment.

```bash
export aws_access_key_id=YOURACCESSIDGOESHERE
export aws_secret_access_key=YOURSECRETKEYGOESHERE
```

## AWS Security Group

Create the EC2 security group `SSH From Anywhere`:

```
[Inbound]
Type=SSH
Protocol=TCP
Port Range=22
Source=0.0.0.0/0

[Outbound]
Type=All traffic
Protocol=All
Port Range=All
Destination=0.0.0.0/0
```

## Spinning up!

```bash
❯ vagrant up

# Optionally provision the machine
❯ vagrant provision

# Do work
❯ vagrant ssh

# Halting the instance
❯ vagrant halt

# Terminating the instance
❯ vagrant destroy
```


Typical output will look like:

```
❯ vagrant --provision up
Bringing machine 'default' up with 'aws' provider...
==> default: Warning! The AWS provider doesn't support any of the Vagrant
==> default: high-level network configurations (`config.vm.network`). They
==> default: will be silently ignored.
==> default: Launching an instance with the following settings...
==> default:  -- Type: t2.micro
==> default:  -- AMI: ami-e251209a
==> default:  -- Region: us-west-2
==> default:  -- Keypair: cv-sandbox
==> default:  -- Security Groups: ["SSH From Anywhere"]
==> default:  -- Block Device Mapping: []
==> default:  -- Terminate On Shutdown: false
==> default:  -- Monitoring: false
==> default:  -- EBS optimized: false
==> default:  -- Source Destination check: 
==> default:  -- Assigning a public IP address in a VPC: false
==> default:  -- VPC tenancy specification: default
==> default: Waiting for instance to become "ready"...
==> default: Waiting for SSH to become available...
==> default: Machine is booted and ready for use!
==> default: Rsyncing folder: /home/clint/libraries/gimme/ => /vagrant
==> default: Running provisioner: ansible...
    default: Running ansible-playbook...

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [default]

TASK [andrewrothstein.bash : resolve platform specific vars] *******************

TASK [andrewrothstein.bash : install bash] *************************************
ok: [default] => (item=bash)
ok: [default] => (item=bash-completions)
ok: [default] => (item=bc)

TASK [andrewrothstein.bash : ensure the bash completions directory exists] *****
ok: [default]

TASK [andrewrothstein.unarchive-deps : resolve platform specific vars] *********

TASK [andrewrothstein.unarchive-deps : install common pkgs...] *****************
ok: [default] => (item=unzip)
ok: [default] => (item=gzip)
ok: [default] => (item=bzip2)
ok: [default] => (item=tar)
ok: [default] => (item=xz)

TASK [miniconda : check for installation of Miniconda] *************************
ok: [default]

TASK [miniconda : download installer...] ***************************************
changed: [default]

TASK [miniconda : installing....] **********************************************
changed: [default]

TASK [miniconda : deleting installer...] ***************************************
changed: [default]

TASK [miniconda : link miniconda...] *******************************************
changed: [default]

TASK [miniconda : update conda pkgs...] ****************************************
skipping: [default]

TASK [miniconda : remove conda-curl since it conflicts with the system curl] ***
ok: [default]

TASK [miniconda : make system default python etc...] ***************************
changed: [default] => (item={'f': 'miniconda.sh', 'd': '/etc/profile.d'})

TASK [install packages managed by `yum`] ***************************************
changed: [default] => (item=['curl', 'docker', 'htop', 'java-1.8.0-openjdk-devel',
    'mlocate', 'parallel', 'pigz', 'tree', 'wget', 'zsh'])

TASK [remove packages managed by `yum`] ****************************************
ok: [default] => (item=['=java-1.7.0-openjdk'])

TASK [install packages managed by `conda`] *************************************
changed: [default] => (item=bwa)
changed: [default] => (item=bwakit)
changed: [default] => (item=fgbio)
changed: [default] => (item=ipython)
changed: [default] => (item=numpy)
changed: [default] => (item=picard)
changed: [default] => (item=samtools)
```
