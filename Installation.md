###Creating an Ubuntu 14.04 Virtual Machine with Vagrant to Use GeoDjango

Vagrant allows a user to work in Linux command line without needing to open a graphical virtual machine interface.

####Create and Connect to Virtual Machine

#####Install Vagrant and VirtualBox

#####Initialize your vagrant directory with:
`$ vagrant init ubuntu/trusty64`

#####Add/turn on a virtual machine with:
`$ vagrant up`

#####Connect to the virtual machine with:
`$ vagrant ssh`

Now you are running an Ubuntu command line.


####Set Up Virtual Machine

#####Install VirtualEnv with:
`$ sudo apt-get install python-virtualenv`

#####Install Python with:
`$ sudo apt-get install python3-dev`

#####Install and configure PostgreSQL with:
```bash
$ sudo apt-get install -y postgresql postgresql-contrib postgresql-server-dev-9.3
$ sudo -u postgres createuser -P [YOUR_USER_NAME]
$ sudo -u postgres createdb -O [YOUR_USER_NAME] [YOUR_DB_NAME]
```

#####Add permissions needed to run Django Tests
```bash
$ sudo -u postgres psql
$ ALTER USER [YOUR_USER_NAME] CREATEDB;
$ ALTER ROLE [YOUR_USER_NAME] SUPERUSER;
$ \q
```

#####Check PostgreSQL
```bash
$ psql -h localhost -U [YOUR_USER_NAME] [YOUR_DB_NAME]
$ \l
$ \q
```

#####Install and configure PostGIS

$ sudo apt-get install -y postgis postgresql-9.3-postgis-2.1
$ sudo -u postgres psql -c "CREATE EXTENSION postgis; CREATE EXTENSION postgis_topology;" [YOUR_DB_NAME]


Install GeoDjango Library Requirements

$ sudo apt-get install libproj-dev gdal-bin


Installations are over, now its time to set a virtual network interface with its own IP and a shared folder

$ exit
$ vagrant halt


Uncomment/edit the following line in the Vagrantfile in your Vagrant directory

config.vm.network "public_network"
config.vm.synced_folder "/Users/vmenezes/projects/gearcircles", "/home/vagrant/project"


Start the server and check the IP of your second interface, this is where your server should run!
User $ python3 manage.py runserver YOURIP:8000 to run the server

$ vagrant up
$ vagrant ssh
$ ifconfig
