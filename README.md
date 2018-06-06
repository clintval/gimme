# Pre-requisites

- Vagrant
- Ansible
- `aws-cli`

# Install

#### Vagrant Plugins

```bash
❯ vagrant plugin install vagrant-env
❯ vagrant plugin install vagrant-aws
```

#### Vagrant Box

```bash
❯ address=http://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-i386-vagrant-disk1.box
❯ vagrant box add aws-dummy "${address}" --provider aws
```

# Environment

Load the following variables into your environment.

```bash
❯ cat credentials
export aws_access_key_id=YOURACCESSIDGOESHERE
export aws_secret_access_key=YOURSECRETKEYGOESHERE`
```
