## Description

A _mostly_ reproducible, _mostly_ persistent, quickly deployable, and portable custom bioinformatics environment built on-demand from anywhere with an SSH client.

This stack is what I use for carefree disposable development environments. Your mileage may vary greatly!

#### Local Dependencies

- [Vagrant](https://www.vagrantup.com/)
- [Ansible](https://www.ansible.com/)
- [EC2](https://aws.amazon.com/ec2/) full-access
- [direnv](https://direnv.net/) (optional)

#### Installation

Ensure you do a recursive clone otherwise you will not pull the submodule roles.

```bash
❯ git clone --recursive https://github.com/clintval/gimme.git
```

#### Vagrant Plugins

```bash
❯ vagrant plugin install vagrant-env
❯ vagrant plugin install vagrant-aws
```

#### Ansible Roles

We will install the miniconda role through `ansible-galaxy`:

```bash
❯ ansible-galaxy install andrewrothstein.miniconda
```

#### Vagrant Box

A dummy box is provided for the `aws` provider. This acts as a pass-through for Vagrant and could be created with defaults.

```bash
❯ address=https://github.com/clintval/gimme/raw/master/example-box/aws-dummy.box
❯ vagrant box add aws-dummy "${address}" --provider aws
```

## Environment

Load the following variables into your environment.

```bash
export AWS_ACCESS_KEY_ID=YOURACCESSIDGOESHERE
export AWS_SECRET_ACCESS_KEY=YOURSECRETKEYGOESHERE
```

Source the file `.envrc`.

## Configuration

This project is set-up to provision an environment very specific to me and will later include some of my [`.dotfiles` ](https://github.com/clintval/.dotfiles/tree/7fa67a8bbbffe678d483dd33c3519e9c15a194cd).

> _Read_: hope you like Zsh!

The bioinformatics tools specified for install are also typical for an environment I use regularly.

## AWS Security Group

Typically, Vagrant is used to spin-up virtual machines which are capable of recieving an SSH connection. In order to enable SSH connection for your EC2 instance we must attach a security group which gives the correct authority.

The security group `SSH From Anywhere` is referenced explicitly in the `Vagrantfile`.

Create the EC2 security group `SSH From Anywhere`:

```ini
[Inbound]
type=SSH
protocol=TCP
port-range=22
source=0.0.0.0/0

[Outbound]
type=All traffic
protocol=All
port-range=All
destination=0.0.0.0/0
```

## Spinning up!

```bash
# Connect to AWS and create the instance
❯ vagrant up

# Provision the instance
❯ vagrant provision

# Do work
❯ vagrant ssh

# Halting the instance
❯ vagrant halt

# Terminating the instance
❯ vagrant destroy
```

Note the first few steps can be combined:

```bash
❯ vagrant --provision up && vagrant ssh
```
