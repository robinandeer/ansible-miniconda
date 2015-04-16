# Miniconda role for Ansible

A role for deploying and configuring [miniconda](http://conda.pydata.org/miniconda.html) and extensions on unix hosts using [Ansible](http://www.ansibleworks.com/).

It can additionally be used as a playbook for quickly provisioning hosts.

Vagrant machines are provided to produce a boxed install of miniconda or a VM for integration testing.

## Usage

Using Ansible Galaxy:

  $ ansible-galaxy install robinandeer.miniconda

And add it to your play's roles:

  - hosts: ...
    roles:
      - robinandeer.miniconda
      - ...

Clone this repo into your roles directory:

    $ git clone https://github.com/robinandeer/ansible-miniconda.git roles/miniconda

And add it to your play's roles:

    - hosts: ...
      roles:
        - miniconda
        - ...

This roles comes preloaded with multiple available defaults. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in ``defaults/main.yml`` for help in configuration. All provided variables start with ``miniconda_``.

You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

    $ ansible-playbook -i inventory --extra-vars='{...}' main.yml

To provision a standalone miniconda box, start the `boxed` VM, which is a Ubuntu 12.04 box:

    $ vagrant up boxed

You will find miniconda listening on the VM's ``$port`` port on address ``192.168.33.20`` in the private network. You can then connect to it as any user. Please note that this is highly insecure, so if you're going to publish this VM you'll want to provide actual authentication.

Run the tests by provisioning the appropriate VM:

    $ vagrant up test-ubuntu-precise

At the moment, ``ubuntu-precise`` is the only test VM available.


## Changelog

### 0.1

Initial version.
