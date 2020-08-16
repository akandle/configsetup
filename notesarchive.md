# TODO: see below
1. Copy this setup into my own setup for actual organic comfort website
	* Essentially just get django running in a new project
	* Will repeat this with Bob's Jobs website 
2. Get running with wagtail (first priority)
	* May experiment with django-crm, later, need prototypes **now**
3. Startup script
	* Environment variables
		* Storage location for VM Docker Host images *Required*
			* `MACHINE_STORAGE_PATH=F:\devdocker\devdocker_images`
	* Initialization
		1. set docker's machine storage env variable
		2. start docker host vm with `docker-machine start ???`
		3. set environment by following directions after running `docker-machine env ???`
		4. Docker is now ready to be used, but only in this specific shell environment

need to run chmod +x ./entrypoint.sh and the production version after editing

Also need to run dos2unix on file before copied over

# TODO: Wishlist
* Gitlab running
	1. Docker containers to try it out
	2. Dedicated VM for gitlab to run "natively" on os
		* TODO: Should a DNS/DHCP/SMTP/etc be running here?
		* Could make into a VM for heavy gitlab install, instead of container inside vm
			* Continue to use containers for lightweight services/development-only services
* Dedicated Docker registry
	* Docker swarm/stacks need images not build files
	* Alter workflow slightly to accomodate building the images independently

==============================================================================================
==============================================================================================
# From a file called notes
# TODO: see below
1. Copy this setup into my own setup for actual organic comfort website
	* Essentially just get django running in a new project
	* Will repeat this with Bob's Jobs website 
2. Get running with wagtail (first priority)
	* May experiment with django-crm, later, need prototypes **now**
3. Startup script
	* Environment variables
		* Storage location for VM Docker Host images *Required*
			* `MACHINE_STORAGE_PATH=F:\devdocker\devdocker_images`
	* Initialization
		1. set docker's machine storage env variable
		2. start docker host vm with `docker-machine start ???`
		3. set environment by following directions after running `docker-machine env ???`
		4. Docker is now ready to be used, but only in this specific shell environment

need to run chmod +x ./entrypoint.sh and the production version after editing

Also need to run dos2unix on file before copied over

# TODO: Wishlist
* Gitlab running
	1. Docker containers to try it out
	2. Dedicated VM for gitlab to run "natively" on os
		* TODO: Should a DNS/DHCP/SMTP/etc be running here?
		* Could make into a VM for heavy gitlab install, instead of container inside vm
			* Continue to use containers for lightweight services/development-only services
* Dedicated Docker registry
	* Docker swarm/stacks need images not build files
	* Alter workflow slightly to accomodate building the images independently




# From a file called structure
Host--> /root/application/build/ /home/docker/project/ <--VM
 *
 * <--  mounted INTO the VM
 *
Dock Host VM /home/docker/project/ <-- mount point for Host /root/application/build/
 *
 * <-- bind mount INTO container
 *
Containers /app <-- mount point for Dock Host VM /home/docker/project


Host Share "host-master-share": F:\app_tech\clients\organic_comfort\pre_alpha_docker_test\image2\app
Docker Volume: host-master-vol ### This what we load into instances of an image as the source files
VM working directory: /home/docker/project


# From a file called example-sites.txt
https://madewithwagtail.org/
https://bootstrapbay.com/?irgwc=1
https://html5up.net/
https://templated.co/
https://bootswatch.com/
https://themeforest.net/category/site-templates
http://www.mojo-themes.com/categories/html-css/
https://graphicburger.com/
https://www.pixeden.com/


# From another file called notes
# Website test notes

## Just done 4-24-19 AM
* create/tested bootlocal.sh
    * mounts shared folder into host vm
* backed up bootlocal.sh into scripts folder
* started documenting "snippets"/scripts
    * oddly in file-copy-to.bat

## TODO Main list for docker work
* Add environment variables for easier life
    * Virtualbox image storage MACHINE_STORAGE_PATH
    * Project root folder APPNAME_ROOT_PATH
    * Project build folder APPNAME_BUILD_PATH
        * This is what will end up being shared to Docker Host VM
    * Docker Machine SSH key APPNAME_SSH_KEY_PATH
* General Needs right now
    * Document "snippets" and scripts
        * scp to and from
        * bootlocal.sh (on host vm, /var/lib/boot2docker/bootlocal.sh)
        * TODO Script for "building"
            * Just move the needed files into a build folder, this will be shared with the docker host vm and then to container
        * TODO start project script
            * sets environment variables on base host
            * starts docker machine
            * sets environment for docker command
            * wishlist: spawns terminals that have enironment inherited
    * FIRST PRIORITY Boot container and bind mount the shared folder on docker host vm
        * This will test the correct term for bind mounting
    * MAIN PRIORITY Simple setup
        * Clean directory
        * Adjust Docker host vm shared folders
            * to use build folder as share
        * build.bat
            * on base host, copies needed files for app to build directory
        * copy personal site to clean directory
        * create venv
        * dockerignore file as needed
        * freeze requirements and create requirements.txt
        * Adjust project to use postgres
            * TODO set static IP of container
            * TODO later, docker networking config
        * dockerfile
            * for django container
        * docker-compose.yml
            * Postgres
            * Django (no wsgi server yet)
                * Entrypoint setup to ensure proper folder mounting
                    * Make sure postgre running and accessible
    * Personal site
        * 

## Source Code

#### General

###### Docker Host VM Info
* Master: dock-host-master
* Slave(s): dock-host-slave-01
* Must bind mount during development
* Shared folder mount point on dock-host-master is /home/docker/app
    * TODO: Will need to determine if cleanup scripts will be needed or just make multople docker host vms?
* Base host projects root: F:\app_tech\clients\\*clientname*\project


or

`TODO: this is a todo`

<!-- TODO: follow for config settings, ignore being among them -->
example config
```
{
    "folders": [],
    "settings": {
        "todoreview": {
            "exclude_folders": [
                "*.git*"
            ]
        }
    }
}
```

## Development setup

#### Requirements
* Docker
* VirtualBox
* Python 3.7+

#### *Optional*
* Pycharm (project files in seperate repo)
* Sublime Text
* Ngrok
* Cmder/GitBash

#### Creation of host VM

* Do not use the docker-machine shared folder setup, does not work
* Replace all vmname with name of choice
    1. Create the VM
        * `docker-machine create --driver virtualbox vmname`
        * or
        * `docker-machine create --driver virtualbox --virtualbox-no-share vmname`
    2. Stop the VM
        * `docker-machine stop vmname`
    3. Edit the shared folders of the VM via virtualbox
        1. Open the settings for the VM just created
        2. In the shared folder settings, add shared folder
            * Folder Path: the path to the shared folder on the main host OS
            * Folder Name: The name of the share, used in VM to mount the share.  No spaces or unusual characters.
            * Auto-mount selected
    4. Start the VM again
        * `docker-machine start vmname`
    5. Mount share in VM
        1. `docker-machine ssh vmname`
        2. Inside VM `mkdir projects`
        3. `sudo mount -t vboxsf -o uid=1000,gid=50 alpha_folder /home/docker/projects/`
        4. Make permenant
            * `sudo vi /mnt/sda1/var/lib/boot2docker/profile`
            * Add the mkdir and mount commands to the end of this file.  Should now auto mount when machine is booted.

#### Environmental Variables
* For now set with a batch file
    * This means that the variables will be specific to the shell instance the file was run in
* Found in environment folder
    * dev.env
    * test.env
    * prod.env

#### To start development session
1. `docker-machine start vmname`
2. `docker-machine env vmname`
    * Run the code output from this command
3. TODO the remainder of this list
3. Rebuild image(s)
4. `docker-compose up` to start compose components
5. profit?


# From a README.md for a python project
# [Organic Comfort][homesite]

**Code for Organic Comfort website**

The live website is located at [www.organiccomfort.com][homesite]

---

# Development Requirements
*TODO: All Version Numbers*


* Python 3.7
* Django 2.2
* VirtualBox
* Docker Engine 18.06 / Docker Compose 3.7
* Ngrok latest

Issues should be filed for incorrect verioning/updates/security patches

# Installation

**Before pulling repo**  
*Install hard dependencies*

1. [Install Python][python]  
*Version 3.7.x*
2. [Install Docker Toolbox][docker]  
*Version 18.x*
3. [Install VirtualBox][vbox]  
*Version 5.2.x*
4. [Install ngrok][ngrok]  
*Latest Version is fine*

*Prepare folder structure and environment*

1. Create root directory  
2. Create Python virtual environment
3. Activate environment
4. Pull application in
5. Run `pip install -r requirments.txt`
6. Run `python -m manage.py makemigrations`
7. Run `python -m manage.py migrate`

# Running Application

1. Ensure that migrations are made if changes to Models occur during development
2. Ensure that the environment created during installation is activated currently
2. `pyton -m manage.py runserver`

# Roadmap

* Pre-Alpha
    * Docker supported infrastructure and services
    * Landing page with minimal user generated data to start
* Alpha
	* 100% code coverage/unit tests/usage test
	* CI System
    * CMS System base
    * Postgres database
    * redis/memcachd in memory store
    * nginx reverse proxy and static asset server
    * HAProxy for load balancing and proxy services
    * Stubs for future growth (Still just ideas for now)
    	* Appointment Scheduler
        * Blog
        * E-Shop
        * E-Magazine/Publishing
        * E-Mail list
        * Forum
        * Organic Database
        * User Profiles
        * Comments/Discussions pertaining to blog posts/products/etc
    * Basic user accounts
        * Administrator
        * Editor/Writer
        * Worker for backing up or other utility services
    * Staging build
* Beta 0.1.0
	* Automated build/test/staging deploy
	* Deterministic configuration of dev/test/stage environments
	* Environmental variable management
	* Secrets managment
	* Core site pages and content ready for production
	* Workable administration
	* Theme/UI/UX design basics implemented
		* Color Pallette chosen
		* General layout chosen
			* Static files created for easy sharing/viewing/critique
				* Or screencaps
			* Implemented in templates
		* Temporary images
	* Major design elements and polished UX drafts and plans ready for Beta 1.0.0
* Beta 1.0.0
	* Goal is production
	* Design finalized
	* Front end focus
		* UI elements and positioning finalized
		* Colors and Fonts finalized
		* Templates complete
		* Automated front end build
			* CSS pre/post processing
			* dependency management
			* packaging
			* minification/compression
	* Testing first class to getting past Beta 1.0
	* Staging code will be run on performant production run time (gunicorn?)
	* CD/CI pipeline able to build per environment

# Progress

Head on over to Trello to see how our sprint is setup.  You can find it [here][trello]

[homesite]: 192.168.0.1:8080/
[python]: https://www.python.org/downloads/
[docker]: https://github.com/docker/toolbox/releases
[vbox]: https://www.virtualbox.org/wiki/Download_Old_Builds_5_2
[ngrok]: https://ngrok.com/download
[trello]: 

==================================================================================================
==================================================================================================

These are just general things

  Create a script to fire up the vms needed for docker
  encorporate into enviro script already being run

Need to actually complete something, get something accomplished
	Learn CPP or Linear CPP ???
	Need to do Data Structures next
	Start crypto
	DHT

Build (packer?) Bunsen image
	manage and use this vm as the primary development environment
	the configuration/instantiation/orchestration will simply be the 
	best way to keep track of the weird little shit that has to be
	tweaked here and there.

	Docker -> workflow and repo
	Git -> workflow and repo (for dev enviro / config shit)

	tmux
	vim


============================================================================
=============================================================================

# Website test notes

## Just done 4-24-19 AM
* create/tested bootlocal.sh
    * mounts shared folder into host vm
* backed up bootlocal.sh into scripts folder
* started documenting "snippets"/scripts
    * oddly in file-copy-to.bat

## TODO Main list for docker work
* Add environment variables for easier life
    * Virtualbox image storage MACHINE_STORAGE_PATH
    * Project root folder APPNAME_ROOT_PATH
    * Project build folder APPNAME_BUILD_PATH
        * This is what will end up being shared to Docker Host VM
    * Docker Machine SSH key APPNAME_SSH_KEY_PATH
* General Needs right now
    * Document "snippets" and scripts
        * scp to and from
        * bootlocal.sh (on host vm, /var/lib/boot2docker/bootlocal.sh)
        * TODO Script for "building"
            * Just move the needed files into a build folder, this will be shared with the docker host vm and then to container
        * TODO start project script
            * sets environment variables on base host
            * starts docker machine
            * sets environment for docker command
            * wishlist: spawns terminals that have enironment inherited
    * FIRST PRIORITY Boot container and bind mount the shared folder on docker host vm
        * This will test the correct term for bind mounting
    * MAIN PRIORITY Simple setup
        * Clean directory
        * Adjust Docker host vm shared folders
            * to use build folder as share
        * build.bat
            * on base host, copies needed files for app to build directory
        * copy personal site to clean directory
        * create venv
        * dockerignore file as needed
        * freeze requirements and create requirements.txt
        * Adjust project to use postgres
            * TODO set static IP of container
            * TODO later, docker networking config
        * dockerfile
            * for django container
        * docker-compose.yml
            * Postgres
            * Django (no wsgi server yet)
                * Entrypoint setup to ensure proper folder mounting
                    * Make sure postgre running and accessible
    * Personal site
        * 

## Source Code

#### General

###### Docker Host VM Info
* Master: dock-host-master
* Slave(s): dock-host-slave-01
* Must bind mount during development
* Shared folder mount point on dock-host-master is /home/docker/app
    * TODO: Will need to determine if cleanup scripts will be needed or just make multople docker host vms?
* Base host projects root: F:\app_tech\clients\\*clientname*\project


or

`TODO: this is a todo`

<!-- TODO: follow for config settings, ignore being among them -->
example config
```
{
    "folders": [],
    "settings": {
        "todoreview": {
            "exclude_folders": [
                "*.git*"
            ]
        }
    }
}
```

## Development setup

#### Requirements
* Docker
* VirtualBox
* Python 3.7+

#### *Optional*
* Pycharm (project files in seperate repo)
* Sublime Text
* Ngrok
* Cmder/GitBash

#### Creation of host VM

* Do not use the docker-machine shared folder setup, does not work
* Replace all vmname with name of choice
    1. Create the VM
        * `docker-machine create --driver virtualbox vmname`
        * or
        * `docker-machine create --driver virtualbox --virtualbox-no-share vmname`
    2. Stop the VM
        * `docker-machine stop vmname`
    3. Edit the shared folders of the VM via virtualbox
        1. Open the settings for the VM just created
        2. In the shared folder settings, add shared folder
            * Folder Path: the path to the shared folder on the main host OS
            * Folder Name: The name of the share, used in VM to mount the share.  No spaces or unusual characters.
            * Auto-mount selected
    4. Start the VM again
        * `docker-machine start vmname`
    5. Mount share in VM
        1. `docker-machine ssh vmname`
        2. Inside VM `mkdir projects`
        3. `sudo mount -t vboxsf -o uid=1000,gid=50 alpha_folder /home/docker/projects/`
        4. Make permenant
            * `sudo vi /mnt/sda1/var/lib/boot2docker/profile`
            * Add the mkdir and mount commands to the end of this file.  Should now auto mount when machine is booted.

#### Environmental Variables
* For now set with a batch file
    * This means that the variables will be specific to the shell instance the file was run in
* Found in environment folder
    * dev.env
    * test.env
    * prod.env

#### To start development session
1. `docker-machine start vmname`
2. `docker-machine env vmname`
    * Run the code output from this command
3. TODO the remainder of this list
3. Rebuild image(s)
4. `docker-compose up` to start compose components
5. profit?
