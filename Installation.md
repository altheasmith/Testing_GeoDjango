###Creating an Ubuntu 14.04 Virtual Machine with Vagrant to Use GeoDjango

Vagrant allows a user to work in Linux command line without needing to open a graphical virtual machine interface.

1. Install Vagrant, VirtualBox, and VirtualEnv

2. Initialize your vagrant directory with:

`$ vagrant init ubuntu/trusty64`

3. Add/turn on a virtual machine with:

`$ vagrant up`

4. Connect to the virtual machine with:

`$ vagrant ssh`


Install minor requirements for our development

$ sudo apt-get install python-virtualenv
$ sudo apt-get install python3-dev


Install and configure PostgreSQL

$ sudo apt-get install -y postgresql postgresql-contrib postgresql-server-dev-9.3

$ sudo -u postgres createuser -P gear_db_user
$ sudo -u postgres createdb -O gear_db_user gearcircles


Add permissions needed to run Django Tests

$ sudo -u postgres plsql
$ ALTER USER gear_db_user CREATEDB;
$ ALTER ROLE gear_db_user SUPERUSER;
$ \q


Check PostgreSQL

$ psql -h localhost -U gear_db_user gearcircles
$ \l
$ \q


Install and configure PostGIS

$ sudo apt-get install -y postgis postgresql-9.3-postgis-2.1
$ sudo -u postgres psql -c "CREATE EXTENSION postgis; CREATE EXTENSION postgis_topology;" gearcircles


Install GeoDjango Library Requirements

$ sudo apt-get install libproj-dev gdal-bin


Installations are over, now its time to set a virtual network interface with its owwn IP and a shared folder

$ exit
$ vagrant halt


Uncoment/edit the following line in the Vagrant file

config.vm.network "public_network"
config.vm.synced_folder "/Users/vmenezes/projects/gearcircles", "/home/vagrant/project"


Start the server and check the IP of your second interface, this is where your server should run!
User $ python3 manage.py runserver YOURIP:8000 to run the server

$ vagrant up
$ vagrant ssh
$ ifconfig
