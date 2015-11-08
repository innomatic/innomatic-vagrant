# Vagrant environment for Innomatic Platform

This project provides a virtual environment for Innomatic Platform 7.x.x applications development using
[Vagrant](https://vagrantup.com).

At this stage this Vagrant environment has been configured to run the Innomatic Legacy stack through the new [Innomatic Platform](https://github.com/innomatic/innomatic-platform). This means that the web server is configured to point the document root to the the innomatic_legacy folder inside the new platform.

Once the new Innomatic Platform is ready, this Vagrant configuration will no more start the legacy stack by default.

You should not use this Vagrant environment for classic Innomatic Legacy stack installations (pre-7.x.x versions) not contained inside the new Innomatic Platform - you should use its own [Vagrantfile](https://github.com/innomatic/innomatic-legacy/blob/develop/Vagrantfile) instead.

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

This Vagrant configurations is already provided in Innomatic Platform inside vagrant folder.

You can also manually install this configuration in a new project. This is also
needed if you are installing Innomatic using composer create-project.

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

After the project is added, you can start the environment like this:

```
$ cd vagrant
$ vagrant up
```

Starting the VM might take some time, since it will download the entire box
and additional applications/library. When the VM is done setting up, point
your browser towards [http://192.168.33.10](http://192.168.33.10) and there you
have it: Innomatic Platform (Legacy stack) tenants desktop access.

To access the Innomatic root control center you should point your browser towards [http://192.168.33.10/root/](http://192.168.33.10/root/).

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
