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
❯ address=http://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-i386-vagrant-disk1.box
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
