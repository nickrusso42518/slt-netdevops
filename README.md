[![Build Status](
https://app.travis-ci.com/nickrusso42518/slt-netdevops.svg?branch=master)](
https://app.travis-ci.com/nickrusso42518/slt-netdevops)

# Safari Live Training - Network DevOps
Source code for the training course. Please contact me with any questions.
Before beginning, be sure you know how to use `git` at a basic level on
your computer. I teach `git` in the course so if you don't know how
to clone this repository yet, do not worry. For this course, only
Linux platforms should be used for the Ansible control/development machine.

> Contact information:\
> Email:    njrusmc@gmail.com\
> Twitter:  @nickrusso42518

  * [Download Instructions](#download-instructions)
  * [Lab Setup](#lab-setup)
  * [Usage](#usage)

## Download Instructions
The easiest way to consume this code is to clone it using SSH or HTTPS.

SSH: `git clone git@github.com:nickrusso42518/slt-netdevops`

or

HTTPS: `git clone https://github.com/nickrusso42518/slt-netdevops`

After cloning, you should see the following file system structure:

```
$ tree --charset=ascii
.
|-- ansible.cfg
|-- hosts.yml
|-- LICENSE
|-- ntp_config.yml
|-- README.md
|-- requirements.txt
|-- requirements.yml
`-- test.yml
```

Ensure you have Python 3.10 or newer installed along with pip. Feel
free to use Python `virtualenv` if you'd like to test multiple versions.

> Visit https://www.python.org/downloads/ to download Python.

`sudo python -m ensurepip`

or

`sudo easy_install pip`

You can install the required packages (really just Ansible and a YAML linter)
using the following command:

`pip install -r requirements.txt`

You should have access to the `ansible` command on the correct version.

```
$ ansible --version
ansible [core 2.16.0]
  config file = /home/ubuntu/slt-netdevops/ansible.cfg
  configured module search path =
    ['/home/ubuntu/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/ubuntu/environments/dec1a/lib/python3.10/site-packages/ansible
  ansible collection location = /home/ubuntu/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/ubuntu/environments/dec1a/bin/ansible
  python version = 3.10.12 (main, Nov 20 2023, 15:14:05) [GCC 11.4.0]
    (/home/ubuntu/environments/dec1a/bin/python)
  jinja version = 3.1.2
  libyaml = True
```

## Lab Setup
If you decide to actively follow along during the course, I recommend
that you deploy (2) Virtual Cisco IOS or IOS-XE devices. You can
use CSR1000v/Cat8000k virtual routers in the cloud, CSR1000v VMware virtual
machines via `.ova` files, simulated environments via EVE-NG, GNS3,
or CML, or perhaps even a real hardware. The only prior configuration
that these devices require is a privilege 15 username and SSH access.
So long as your Ansible control machine can SSH into these devices,
you can follow along with course. For continuous integration to work,
these network devices need to be accessible over the Internet. For that
reason, I recommend using public clouds such as AWS, Azure, or GCP.

## Usage
This repository is kept minimal since the main point of this course is
teaching the fundamentals of Network DevOps, not Ansible as a specific tool.
  * To edit NTP server variables, open `hosts.yml` and update the
    `ntp_server` variables using valid IPv4 addresses.
  * To run the playbook, run `ansible-playbook ntp_config.yml` from the shell.
  * To test the playbook, run `ansible-playbook test.yml` from the shell. This
    mimics what Travis CI does each time code is committed to Github.

If you are connecting to devices that that only support legacy SSH options,
try adding this configuration to `~/.ssh/config`:

```
Host *
        KexAlgorithms +diffie-hellman-group1-sha1,diffie-hellman-group14-sha1
        HostKeyAlgorithms=+ssh-dss,ssh-rsa
        PubkeyAcceptedKeyTypes=+ssh-rsa
```
