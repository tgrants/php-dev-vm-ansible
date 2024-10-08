# PHP development VM configuration with ansible for students

## Features

* Lightweight
	* uses Xfce
	* ~4 GiB virtual disk size with Virtualbox
* Includes various tools
	* PHP and Composer
	* MariaDB and sqlite3
	* VSCode and Git

## Instructions

* Create the virtual machine:
	* Install [Debian](https://www.debian.org/) on a [Virtualbox](https://www.virtualbox.org/) VM
		* Create users (or update `hosts`)
			* Set root password to `changeme`
			* Create `user` with password `changeme`
		* Software selection - select only `SSH server`
	* Prepare the VM for ansible
		* Make sure you can ssh into the VM
			* Update VM network settings `Machine > Settings > Network > Attached to > Bridged Adapter`
			* Get the ip address with `ip a` and update `hosts`
			* Copy key by SSH-ing into the VM `ssh user@192.168.x.y`
		* Install packages and add sudo privileges to user
			* Log in as root with `su -` and install packages `apt install sudo python3`
			* Add user to sudoers `adduser user sudo`
	* Setup the VM `ansible-playbook playbooks/setup.yml`
* Trim virtual disk:
	* Remove all unnecessary files `ansible-playbook playbooks/cleanup.yml`
	* On VM:
		* `sudo dd if=/dev/zero of=/bigemptyfile bs=4096k status=progress`
		* `sudo rm -f /bigemptyfile`
	* On host:
		* `vboxmanage modifymedium /mnt/storage/VBOX/phpdev/phpdev.vdi --compact`
			* edit the path to match your .vdi file

## Other information

### Changelog

To see changes, see [Releases](https://github.com/tgrants/php-dev-vm-ansible/releases) in Github.

### License

This repository is licensed under `The Unlicense`. See `LICENSE` for more information.
