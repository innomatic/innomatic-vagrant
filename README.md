# Vagrant environment for Innomatic Platform

This project provides a virtual environment for Innomatic Platform 7.x.x
applications development using [Vagrant](https://vagrantup.com).

You should not use this Vagrant environment for pre-7.x.x Innomatic Legacy
stack installations - you should use their own
[Vagrantfile](https://github.com/innomatic/innomatic-legacy/blob/master/Vagrantfile)
instead.

## What's in the box?

When you start Vagrant, this environment will provide the following tools
that can be useful when developing for Innomatic Platform:

- Git
- cURL
- MySQL
  * Username: `root`
  * Password: empty
- nginx
- PHP
- PHP-FPM
- APC
- XDebug

Other components:
- RabbitMQ
- PEAR
- SQLite

## Usage and requirements

### Ansible

[Ansible](http://ansible.com) is used to provision the virtual machine, so you
must have that installed. Follow the
[installation instructions](http://docs.ansible.com/intro_installation.html#installation).

### Usage

Installation is as easy as cloning a GitHub project:

```
$ cd your-innomatic-project
$ git clone https://github.com/innomatic/innomatic-vagrant.git vagrant
```

Or, if you're using Git already in your project, you can use it as a submodule:

```
$ cd your-innomatic-project
$ git submodule add https://github.com/innomatic/innomatic-vagrant.git vagrant
```

After the project has been added, you can start the environment like this:

```
$ cd vagrant
$ vagrant up
```

Starting the VM might take some time, since it will download the entire box
and additional applications/library.

### Innomatic setup

When the VM is done setting up, enter the vagrant box and launch composer
install like this:

```
$ vagrant ssh
$ cd /var/www
$ composer install
```

Then point your browser towards [http://192.168.33.10](http://192.168.33.10)
and follow the Innomatic web setup procedure using the following MySQL user:

* Username: `root`
* Password: empty

At the end of the web setup you are redirected to the tenant desktop login
page.

Before accessing a tenant desktop, you need to create at least a tenant using
the Innomatic root control center desktop or through the tenants CLI script.

To access the Innomatic root control center you should point your browser
towards [http://192.168.33.10/root/](http://192.168.33.10/root/) with the
following credentials:

* Username: `root`
* Password: the one you provided during the web setup phase

Full Innomatic Platform installation instructions can be found
[here](https://innomatic.atlassian.net/wiki/display/IMP/Installation+and+Upgrade+Guides).

#### Note

If you're using Windows, you have to modify the `Vagrantfile` a little bit to
make it all work (since Windows doesn't support NFS). Replace the following
lines in the Vagrantfile:

```ruby
config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", :nfs => true
config.vm.synced_folder "..", "/var/www", id: "application",  :nfs => true
```

with:

```ruby
config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root"
config.vm.synced_folder "..", "/var/www", id: "application"
```

## License

```
Copyright (c) 2014, Ramon Kleiss <ramon@cubilon.nl>
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

The views and conclusions contained in the software and documentation are those
of the authors and should not be interpreted as representing official policies,
either expressed or implied, of the FreeBSD Project.
```
