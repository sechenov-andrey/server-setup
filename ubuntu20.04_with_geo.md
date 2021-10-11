Ubuntu (20.04) Server Set Up for Django with GDAL Instruction
============================================================

Create user, setup SSH
----------------------

Connect through SSH to remote server and update repositories and install some initial needed packages:

sudo apt-get update ; \
sudo apt-get install -y vim mosh tmux htop git curl wget unzip zip gcc build-essential make

Configure SSH:

sudo vim /etc/ssh/sshd_config
    AllowUsers www
    PermitRootLogin no
    PasswordAuthentication no

Restart SSH server, change www user password:

sudo service ssh restart
sudo passwd www

Init — must-have packages & ZSH
-------------------------------

sudo apt-get install -y zsh tree redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python3-pip libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev supervisor
Install oh-my-zsh:

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

Install postgresql
------------------

sudo apt install postgresql postgresql-contrib

sudo -i -u postgres

psql

'''
postgres@37-140-199-138:~$ psql
psql (12.8 (Ubuntu 12.8-0ubuntu0.20.04.1))
Type "help" for help.

postgres=# \q
'''
пользователь для Джанго

postgres@37-140-199-138:~$ dropuser django
postgres@37-140-199-138:~$ createuser -W --interactive django
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n
Password: 
postgres@37-140-199-138:~$ 

install gdal libriries
sudo apt-get install binutils libproj-dev gdal-bin

add-apt-repository ppa:ubuntugis/ppa
apt-get update

apt install postgis postgresql-postgis

➜  ~ sudo -i -u postgres           
postgres@37-140-199-138:~$ psql
psql (12.8 (Ubuntu 12.8-0ubuntu0.20.04.1))
Type "help" for help.

postgres=# CREATE EXTENSION postgis;
CREATE EXTENSION
postgres=# \q
postgres@37-140-199-138:~$ exit
logout
➜  ~ 
