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
have it: Innomatic Platform (Legacy stack).

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

## Versioning

This project is versioned using [Semantic Versioning](http://semver.org/spec/v1.0.0.html):

```
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to
be interpreted as described in RFC 2119.

Software using Semantic Versioning MUST declare a public API. This API could
be declared in the code itself or exist strictly in documentation. However
it is done, it should be precise and comprehensive.

A normal version number MUST take the form X.Y.Z where X, Y, and Z are
integers. X is the major version, Y is the minor version, and Z is the patch
version. Each element MUST increase numerically by increments of one. For
instance: 1.9.0 -> 1.10.0 -> 1.11.0.

When a major version number is incremented, the minor version and patch
version MUST be reset to zero. When a minor version number is incremented,
the patch version MUST be reset to zero. For instance: 1.1.3 -> 2.0.0 and
2.1.7 -> 2.2.0.

A pre-release version number MAY be denoted by appending an arbitrary string
immediately following the patch version and a dash. The string MUST be
comprised of only alphanumerics plus dash [0-9A-Za-z-]. Pre-release versions
satisfy but have a lower precedence than the associated normal version.
Precedence SHOULD be determined by lexicographic ASCII sort order. For
instance: 1.0.0-alpha1 < 1.0.0-beta1 < 1.0.0-beta2 < 1.0.0-rc1 < 1.0.0.

Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications must be released as a new version.

Major version zero (0.y.z) is for initial development. Anything may change
at any time. The public API should not be considered stable.

Version 1.0.0 defines the public API. The way in which the version number
is incremented after this release is dependent on this public API and how
it changes.

Patch version Z (x.y.Z | x > 0) MUST be incremented if only backwards
compatible bug fixes are introduced. A bug fix is defined as an internal
change that fixes incorrect behavior.

Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. It MAY be
incremented if substantial new functionality or improvements are introduced
within the private code. It MAY include patch level changes. Patch version
MUST be reset to 0 when minor version is incremented.

Major version X (X.y.z | X > 0) MUST be incremented if any backwards
incompatible changes are introduced to the public API. It MAY include minor
and patch level changes. Patch and minor version MUST be reset to 0 when
major version is incremented.
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
