# Demo: `cm-update-server`

This repo is a Vagrant-based demo server for xdarklight's [Cyanogenmod
Update Server](https://github.com/xdarklight/cm-update-server), which is
a open source implementation of the Cyanogenmod REST API used by the
CMUpdater app. It allows monitoring and installation of both full and
incremental updates to arbitrary custom ROMs.

This is still a work in progress.

### Usage

After installing [Vagrant](https://www.vagrantup.com/downloads) and
[Virtualbox](https://www.virtualbox.org/wiki/Downloads):

```
vagrant plugin install vagrant-berkshelf
vagrant plugin install vagrant-omnibus
vagrant plugin install vagrant-cachier # Optional

vagrant up
```

You now have a local Virtualbox VM running at
`http://localhost:3000/api`. You will need to log in via `vagrant ssh`
and follow the `cm-update-server` README instructions in order add ROMs.

### Sample

```
vm~$ vagrant ssh
vm~$ sudo bash
vm~$ cd /opt/nodejs/cm-update-script
vm~$ node add-build.js --device grouper --filename some-file.zip --md5sum 0dff54e10853eb8fcf37ecef9cf1bd4b --channel SNAPSHOT --api_level 19 --timestamp 1415780513 --incrementalid 2e6a32151e --active --subdirectory grouper-11.0
vm~$ exit
host~$ curl 127.0.0.1:3000/api --data '{"method":"get_all_builds","params":{"device":"grouper","channels":["snapshot"]}}'
```
