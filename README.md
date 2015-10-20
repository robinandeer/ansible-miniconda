# Miniconda role for Ansible [![Build Status][travis-image]][travis-url]

A role for deploying and configuring [miniconda](http://conda.pydata.org/miniconda.html) and extensions on unix hosts using [Ansible](http://www.ansibleworks.com/).

It can additionally be used as a playbook for quickly provisioning hosts.

Vagrant machines are provided to produce a boxed install of miniconda or a VM for integration testing.

## Usage

Using Ansible Galaxy:

```bash
$ ansible-galaxy install robinandeer.miniconda
```

And add it to your play's roles:

```yaml
- hosts: ...
  roles:
    - robinandeer.miniconda
    - ...
```

Clone this repo into your roles directory:

```bash
$ git clone https://github.com/robinandeer/ansible-miniconda.git roles/miniconda
```

And add it to your play's roles:

```yaml
- hosts: ...
  roles:
    - miniconda
    - ...
```

This roles comes preloaded with multiple available defaults. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in ``defaults/main.yml`` for help in configuration. All provided variables start with ``miniconda_``.

You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

```bash
$ ansible-playbook -i inventory --extra-vars='{...}' main.yml
```

To provision a standalone miniconda box, start the `boxed` VM, which is a Ubuntu 12.04 box:

```bash
$ vagrant up boxed
```

You will find miniconda listening on the VM's ``$port`` port on address ``192.168.33.20`` in the private network. You can then connect to it as any user. Please note that this is highly insecure, so if you're going to publish this VM you'll want to provide actual authentication.

Run the tests by provisioning the appropriate VM:

```bash
$ vagrant up test-ubuntu-precise
```

At the moment, ``ubuntu-precise`` is the only test VM available.

## Contributors
- Koji Tanaka ([kjtanaka](https://github.com/kjtanaka))

## Credits
I took on the challenge to write my own distributable Ansible role to learn more about the tool. As such, I've taken in extensive inspiration from the following projects:

- [SciLifeLab/deployment][deployment] for the included miniconda role
- [nicholsn/ansible-role-miniconda][nicholsn]
- [zenoamaro/ansible-role-template][template] as a base role template


## Changelog

### 0.6
- Avoid re-download of installer if conda exists

### 0.5
- only update conda when initially installing miniconda

### 0.4
- use ``lininfile`` to add miniconda to ``$PATH``

### 0.3
- add option to specify rcfile to modify ``$PATH``

### 0.2
- add option to modify ``.bashrc``
- add option to add ``.condarc`` to the system

### 0.1
- Initial version.


[deployment]: https://github.com/SciLifeLab/deployment
[nicholsn]: https://github.com/nicholsn/ansible-role-miniconda
[template]: https://github.com/zenoamaro/ansible-role-template
[travis-url]: https://travis-ci.org/robinandeer/ansible-miniconda
[travis-image]: https://img.shields.io/travis/robinandeer/ansible-miniconda.svg?style=flat
