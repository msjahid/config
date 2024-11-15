# Kali Linux Setup and Customization Guide

This guide includes steps to resolve font issues, configure Guake for autostart, install fonts, and perform other customizations on Kali Linux.

## 1. Fixing Language Font Issues

To enable Bengali (Bangladesh) fonts, follow these steps:

```bash
sudo vim /etc/locale.gen
```

- Find the line with bn_BD UTF-8.
- Uncomment it (remove the #).
- Save and exit, then run the following command to generate locales:

```bash
sudo locale-gen
```

This will enable Bengali language support for your system.


## 2. Autostart Guake Terminal
To set Guake to autostart on login, create a symbolic link in the autostart directory:

```bash
sudo ln -s /usr/share/applications/guake.desktop /etc/xdg/autostart/
```
This ensures that Guake launches automatically when the system starts.

## 3. Install Font Manager
To install a font manager on Kali Linux, use:

```bash
sudo apt install font-manager -y
```
This allows you to manage your fonts easily. (Eg. Cascadia.ttf)

## 4. Customize Guake Color Palette
To change Guake's color palette:

- Top color: #62A0EA
- Bottom color: #2E3440

These colors can be set via the Guake preferences under the "Appearance" section.

## 5. Add Asterisks to Password View
To enable password feedback (show asterisks as you type passwords):

5.1: Open a new terminal window (Ctrl + Alt + T) and enter:

```bash
sudo visudo
```

5.2: Use the keyboard or mouse to scroll to the line that reads:

```bash
Defaults env_reset
```

5.3: Move the cursor to the end of the line and add:

```bash
Defaults env_reset,pwfeedback
```

5.4: Save the changes by pressing `Ctrl + X`, then `Y`, followed by `Enter`.

## 6. Enable Bluetooth on Boot
To ensure Bluetooth starts automatically on boot:

```bash
sudo systemctl enable bluetooth.service
```

This command enables the Bluetooth service to start on boot, allowing you to use Bluetooth devices without manually starting the service.

## 7. Install and Use Asciinema for Terminal Recording
To install Asciinema for terminal recording:

```bash
sudo apt install asciinema
```

To authenticate with Asciinema:

```bash
asciinema auth
```

Record your terminal session:

```bash
asciinema rec demo.cast
```

Replay the recording:

```bash
asciinema play demo.cast
```

Upload the recording to Asciinema.org:

```bash
asciinema upload demo.cast
```

## 8. Convert Asciinema Recordings to GIF
To convert your Asciinema recordings into a GIF, follow these steps:

8.1: Install Cargo (Rust package manager):

```bash
sudo apt-get install cargo
```

8.2: Install `agg` to convert recordings into GIF format:

```bash
cargo install --git https://github.com/asciinema/agg
```

8.3: Add the Cargo bin directory to your `PATH` by editing `~/.bashrc` (or `~/.zshrc` for Zsh users):

```bash
export PATH="$HOME/.cargo/bin:$PATH"
```

8.4: Source the file to apply changes:

```bash
source ~/.bashrc  # or source ~/.zshrc for Zsh users
```

You can now use `agg to` convert your `.cast` files to `.gif` format for easy sharing.

```bash
agg https://asciinema.org/a/597290 test.gif
```

## 9. Docker Setup for First-Time Use
For first-time Docker use:

```bash
docker-compose build
```

If you encounter any errors, clear previous caches:

```bash
docker-compose down --volumes --rmi all
```

Rebuild the image to resolve any inconsistencies:

```bash
docker-compose build --no-cache
```

Then, bring up the containers:

```bash
docker-compose up
```

This will start the services defined in your `docker-compose.yml` file.

# Docker Troubleshooting Guide

This guide helps you resolve issues with Docker and Docker Compose, especially related to Docker daemon, permissions, and port conflicts.

## 1. Check Docker Daemon Status

Ensure Docker is running on your system. You can do this by checking the Docker service status:

```bash
sudo systemctl status docker
```

If it's not running, start the Docker service:

```bash
sudo systemctl start docker
```


## 2. Enable Docker to Start on Boot
If Docker is not set to start on boot, you can enable it:

```bash
sudo systemctl enable docker
```

This will ensure Docker starts automatically when the system boots up.

## 3. Verify Docker Socket Permissions

The issue may be caused by insufficient permissions to access the Docker socket. To check the permissions:

```bash
ls -l /var/run/docker.sock
```

Make sure the user has permission to access the socket. If not, add your user to the Docker group:

```bash
sudo usermod -aG docker $USER
```

After running this command, log out and log back in to refresh the group membership, or restart the system.

## 4. Restart Docker Daemon

Sometimes restarting the Docker daemon can resolve issues:

```bash
sudo systemctl restart docker
```

## 5. Check Docker Configuration

### List Running Containers

To view only the containers currently running:

```bash
sudo docker ps
```

### List All Containers (Running and Stopped)

To see all containers, including stopped ones:

```bash
sudo docker ps -a
```

If you want you can Stop the Specific Container: If you know which container might be using port '(eg. PORT-4000 & CONTAINER-1746fbc94449)', stop it using:

```bash
sudo docker stop 1746fbc94449
```

### Inspect Specific Container Details

To get more detailed information about a specific container, use:

```bash
docker inspect 1746fbc94449
```

## 6. Fix Port Conflicts

If you get an error like:

> [!CAUTION]
> driver failed programming external connectivity on endpoint loan-approval-app (0e6303b4f4b0294f1ebe7f4311b2b243d945ff4fd425138892d318130c491178): failed to bind port 0.0.0.0:4000/tcp: Error starting userland proxy: listen tcp4 0.0.0.0:4000: bind: address already in use

Run the following to identify the process using port 4000:

```bash
sudo lsof -i :4000
```

Then kill the process by running: `(eg. PID-53348)'

```bash
kill -9 <PID>
```

Where `<PID>` is the process ID you found from the previous command.

## Conclusion

These steps should help you troubleshoot and resolve common Docker issues related to the Docker daemon, permissions, and port conflicts.


# Linux Software Install Commands
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt install gnome-shell-extensions
sudo apt install net-tools
sudo apt install gnome-tweaks
sudo apt install htop
sudo apt-get install snapd
sudo apt install python3-pip
sudo apt install spyder
```

## Xampp and Mysql 
Launch Xampp through the Terminal
```bash
sudo /opt/lampp/lampp start
```

Open xampp MySQL as mysql -u root -p so adding path in bashrc file
```bash
export PATH=/opt/lampp/bin/:$PATH
```
Then close it and source it with:
```bash
source ~/.bashrc
```
Adding password Xampp and MySQL, phpMyAdmin
```bash
sudo /opt/lampp/lampp security
```
Open xampp GUI through the terminal
```bash
sudo /opt/lampp/manager-linux-x64.run
```
## Back up MySQL or MariaDB database
to back up the database to a file called **mydata-backup.sql**, use the following command syntax. This will prompt you for a password when entering the command.
```bash
mysqldump -u root -p mydata > mydata-backup.sql
```
If you need to avoid the password prompt, such as the case in a Bash script, then you can put the password into the command itself by using the **--password** option.
```bash
mysqldump -u root --password="mypassword" mydata > mydata-backup.sql
```
to back up the database to some other location than your present working directory, just put the path in your command.
```bash
mysqldump -u root -p mydata > /home/linuxconfig/mysql/mydata-backup.sql
```
to back up more than one database at once, you can list them separately in your command after the **--databases** option. In this example, we will backup the databases **mydata** and **accounting**.
```bash
mysqldump -u root -p --databases mydata accounting > mydata-backup.sql
```
You can also make a backup of every MySQL or MariaDB database at once by specifying the **--all-databases** option.
```bash
mysqldump -u root -p --all-databases > mydata-backup.sql
```
## Restore a MySQL or MariaDB database backup
This command will restore our database data to our mydata database from previous examples.
```bash
mysql -u root -p mydata < mydata-backup.sql
```
If your backup file contains multiple databases, you can select which ones to restore by using the --one-database flag in your command.
```bash
mysql --one-database mydata < mydata-backup.sql
```
## Neovim install configure 
At first install Neovim
```bash
sudo apt install neovim
```
Prerequisite system files
```bash
sudo apt-get install curl
sudo apt-get install git
sudo apt install exuberant-ctags
pip3 install jedi
```
**Node.js v18.x**:

```sh
# Using Ubuntu
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g yarn
```
configure neovim in config folder
```bash
cd .config 
mkdir nvim 
cd nvim 
nvim init.vim
mkdir autoload
cd autoload
curl https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
curl https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim -o plug.vim
```
Then install plugin on your neovim
```bash
:PlugInstall
```
Plugin Open command
```bash
:NERDTreeToggle
:TerminalSplit bash
:TagbarToggle
```
Python install
```bash
cd plugged/coc.nvim/
yarn install
yarn build
:CocInstall coc-python
```
## Create Project of JavaScript
```bash
mkdir nodeproject
cd nodeproject/
yarn init
yarn add express
yarn # if you delete some items then type yarn can back items
touch index.js
```
Expree Code for first time
```JavaScript
const express = require('express')
const app = express()

app.get("/",(req,res)=>{
    res.end("Hello World")
})

app.listen(4000)
```
Debug true mode for developing 
```bash
yarn global add nodemon
#just run your code insted of node to nodemon
```
**Nodemon use in npm or yarn command**:
```bash
sudo npm install -g nodemon
#or
sudo yarn global add nodemon
sudo nodemon -v
```
## Git

###### Cloning remote
```
git clone remote_link 
```
###### Initialize local git repo
```
git init 
```
###### Add all files to index
```
git add .
```
###### Check status of working tree
```
git status
```
###### Commit changes in index
```
git commit -m 'messages'
```
###### Push to remote repo
```
git push
```
###### Push with remote name
```
git push -u origin branch-name
```
###### Pull latest from remote repo
```
git pull
```
###### Clone repo into a local new directory
```
git clone
```
###### Switching branch
```
git checkout branch-name
```
###### Merging branch
```
git merge branch-name
```
###### View information about previous commits that have occurred recent
```
git log
```
###### Displaying individual links of origins
```
git remote -v 
```
###### Setting Global Username
```
git config --global user.name "msjahid"
```
###### Setting Global Email
```
git config --global user.email "msjahid.ai@gmail.com" 
```
###### Check username, email
```
git config --global user.name
```
```
git config --global user.email
```
--------------------------------------------------------------------------------

## Heroku

###### Login
```
heroku login
```
###### Create App
```
heroku create app-name
```
###### Push App
```
git push heroku main
```
###### Bash Access
```
heroku run bash
```
```
ls
```
```
cd /
```
```
ls
```
```
exit
```
###### Setup Heroku PostgreSQL Database
```
heroku addons:create heroku-postgresql:hobby-dev
```
###### Access Heroku PostgreSQL Database
```
heroku pg:credentials:url --app app-name
```
###### Heroku + Django: Collect Static Files (No need if collected from locally)
```
heroku run python manage.py collectstatic
```

--------------------------------------------------------------------------------

## Django

###### Create virtualenv
```
python3 -m venv venv
```
```
source venv/bin/activate
```
###### Install django
```
pip3 install django
```
```
python3 -m django --version
```
###### Create Project
```
django-admin startproject project-name
```
###### Create Project Using Current Dir
```
django-admin startproject project_name .
```
###### Create App
```
python manage.py startapp app-name
```
###### Create superuser
```
python manage.py createsuperuser
```
###### Database
```
python manage.py makemigrations
```
```
python manage.py migrate
```
###### Runserver
```
python manage.py runserver
```
###### Shell
```
python manage.py shell
```
###### Flush database
```
python manage.py flush
```
###### Requirements
```
pip3 freeze
```
```
pip3 list
```
```
pip3 freeze > requirements.txt
```
```
pip3 install -r requirements.txt
```

--------------------------------------------------------------------------------

## NPM

###### Install
```
npm install
```
###### Compiles and hot-reloads for development
```
npm run serve
```
###### Compiles and minifies for production
```
npm run build
```
```
npm run build --watch
```
###### Remove caches and reinstall 
```
rm -rf node_modules package-lock.json && npm install
```

--------------------------------------------------------------------------------

## Docker

* Docker-Compose

###### Build
```
docker-compose build --no-cache --force-rm
```
###### Push
```
docker-compose push
```
###### Pull
```
docker-compose pull
```
###### Up
```
docker-compose up
```
###### Down
```
docker-compose down
```
###### Up, Down (run in background)
```
docker-compose up -d
```
```
docker-compose down -d
```

* Docker

###### Image list
```
docker images
```
###### Container list
```
docker container ls -a
```
###### Stop Container
```
docker container stop container_id
```
###### Process list
```
docker ps -a
```
###### Remove images
```
docker image rm image_id_1 image_id_2 image_id_3
```
###### Remove Container
```
docker container rm container_id
```
* Project Related (from project directory)

###### Show Images
``` 
docker-compose images
```
###### All Commands
```
docker-compose
```
###### Pull
```
docker-compose pull
```
###### Migrate
```
docker-compose run my_service_name python manage.py migrate
```
###### Faker
```
docker-compose run my_service_name python fake_data.py (if available)
```
###### Up
```
docker-compose up
```   
###### Show host ip
```
docker-compose exec my_service_name bash
```
```
hostname -i
```
```
docker-compose exec my_db_service_name bash
```
```
hostname -i   
```
* Manage docker as a non-root user (post-installation steps for linux)

###### 1. Create the docker group
```
sudo groupadd docker
```
###### 2. Add your user to the docker group
```
sudo usermod -aG docker $USER
```
###### 3. Log out and log back in so that your group membership is re-evaluated
```
newgrp docker 
```
###### 4. Verify that you can run 'docker' commands without 'sudo'
```
docker run hello-world
```

--------------------------------------------------------------------------------

## Linux

###### Logging in as root
```
ssh root@your_server_ip
```
###### Creating a new user
```
adduser siyam
```
###### Granting administrative privileges
```
usermod -aG sudo siyam
```
###### Logging in as user
```
ssh root@siyam
```
###### Free up disk space
```
sudo du -sh /var/cache/apt
```
```
sudo apt-get clean
```
###### User permission
```
sudo chown -R $USER:$USER ./
```
###### Blank screen fix (lightdm)
```
Ctrl + Alt + F4
```
```
your username & password
```
```
sudo apt-get purge lightdm
```
```
sudo apt-get update
```
```
sudo apt-get install lightdm 
```
```
dpkg-reconfigure lightdm
```
```
sudo shutdown -r now 
```
###### Reboot immediately with killing all the processes
```
sudo shutdown -r now 
```
###### Reboot
```
sudo reboot
```
###### Power off
```
sudo poweroff
```
###### Systemctl
```
sudo systemctl status package_name
```
```
sudo systemctl enable package_name
```
```
sudo systemctl start package_name
```
```
sudo systemctl stop package_name
```
```
sudo systemctl disable package_name
```
###### Remove directory
```
sudo rm -rf dir_name
```
###### View file
```
cat file_name
```
###### Edit file
```
vim file_name
```
```
gedit file_name
```
###### Copy
```
cp file.txt /backup
```
```
cp file.txt /backup/new_file.txt
```
```
cp file.txt dir file1.txt file2.txt dir1
```
###### Move
```
mv testfile testfile2
```
```
mv /home/jack/testfile /home/jack/testfile2
```
```
mv /home/jack/testfile /home/jack/Documents/
```
###### Restart apache for server
```
sudo systemctl restart apache2
```

--------------------------------------------------------------------------------

## PostgreSQL Setup on Linux

###### Install
```
sudo apt update
```
```
sudo apt install postgresql postgresql-contrib
```
###### Start service
```
sudo service postgresql start
```
###### Check status
```
sudo systemctl status postgresql
```
###### Login postgres with password
```
sudo -i -u postgres
```
```
psql
```
###### Connection details
```
postgres=# \conninfo
```
###### Exit prompt
```
postgres=# \q
```
###### Login direct
```
sudo -u postgres psql
```
###### Set password
```
CREATE USER postgres WITH PASSWORD 'postgres';
```
###### Create database
```
CREATE DATABASE database_name;
```
###### Set permissions
```
GRANT ALL PRIVILEGES ON DATABASE postgres TO postgres;
```
###### Database list
```
postgres=# \l
```
**Secure PostgreSQL**:
```bash
sudo passwd postgres
# su - postgres 
psql -c "ALTER USER postgres WITH PASSWORD 'secure_password_here';" 
exit
sudo systemctl restart postgresql 
```
### pgAdmin 4 install
```bash
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add -
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt update
sudo apt install pgadmin4 
```
Configure PgAdmin4 after installing Add New Server > General > Name > 'localhost'> connection Host name/address > 127.0.0.1 
fixed error for the password open terminal

```bash
sudo -i -u postgres
$ psql
\password postgres
# Enter your password 
```

Fixed error in W: Key is stored in legacy trusted.gpg keyring
```bash
cd /etc/apt
sudo cp trusted.gpg trusted.gpg.d
```

## Gimp install with GMIC and Resynthesizer  
Launch Terminal and following these below command
```bash
sudo apt install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
sudo flatpak install https://dl.flathub.org/repo/appstream/org.gimp.GIMP.flatpakref
sudo flatpak install org.gimp.GIMP.Plugin.GMic//2-40
sudo flatpak install org.gimp.GIMP.Plugin.Resynthesizer//2-40
sudo flatpak install org.gimp.GIMP.Plugin.BIMP//2-40
```
# Machine Learning Tools & Library
```bash
pip3 install pandas
pip3 install numpy
pip3 install scipy
pip3 install -U scikit-learn
pip3 install seaborn
pip3 install streamlit
```
**Jupyter Autocomplete Extension**:
```bash
pip3 install jupyter_contrib_nbextensions && jupyter contrib nbextension install
pip3 install jupyter-tabnine --user
jupyter nbextension install --py jupyter_tabnine --user
jupyter nbextension enable --py jupyter_tabnine --user
jupyter serverextension enable --py jupyter_tabnine --user
```
**Jupyter Themes**:
```bash
pip3 install jupyterthemes
pip3 install --upgrade jupyterthemes
jt -l #list of all themes
jt -t chesterish
```

**Jupyter ipynb to pdf**:
```bash
sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-plain-generic
export PATH=/Library/TeX/texbin:$PATH # if path missing default no need
jupyter nbconvert --execute --to pdf test.ipynb
```

**Jupyter Markdown Image**:
```bash
![alt](population-variance.png) | ![alt](sample-variance.png)

<table><tr>
<td> <img src="test.png" alt="Drawing" style="width: 500px;"/> </td>
<td> <img src="test2.png" alt="Drawing" style="width: 500px;"/> </td>
</tr></table>
```


## How to Work With JSON in Your Terminal With fx
```bash
sudo apt install curl
npm install -g fx
# *** Insted of npm use sudo snap install fx
```
**use fx command**:
```bash
curl https://api.coindesk.com/v1/bpi/currentprice.json | fx .
```
# Python Specific version install not mandatory
```bash
sudo apt-get install libssl-dev openssl
wget https://www.python.org/ftp/python/3.5.0/Python-3.10.4.tgz
tar xzvf Python-3.10.4.tgz
cd Python-3.10.04
./configure
make
sudo make install
```
**Python idle specific version**:
```bash
sudo apt-get install idle-python3.10
```
## Install the network scanning tool Nmap
```bash
sudo apt install nmap
```
Now find your ip address using the *ifconfig'* command
```bash
nmap -sP 192.168.12.208/24
```
## Git configure
```bash
git config --global user.name "msjahid" 
git config --global user.email "msjahid.ai@gmail.com"
# Checking command
git config --global user.name
git config --global user.email
```
## Mongodb Warning 
```bash
echo "deb http://security.ubuntu.com/ubuntu impish-security main" | sudo tee /etc/apt/sources.list.d/impish-security.list
sudo apt-get update
sudo apt-get install libssl1.1
```
## Heroku Postgresql Postbird
```bash
postgres://ogighaslynkoep:0625ef9b305e7768c170ecab1b69a3e3f03450368adb1f08100d3465cd68ca5a@ec2-44-205-41-76.compute-1.amazonaws.com:5432/dfj7frahkcae9k?ssl=verify-full
```
Other software "ssl=no-verify" if not working then use settings>Config Vars>add Key {GSSLMODE}, value{no-verify}

## CSVfile readable, nbterm, pgcli, jupytext
Read the full [CSVKit](https://csvkit.readthedocs.io/en/0.9.1/index.html) offical documentation.

```bash
pip install csvkit
# for multiple python version
python3.10 -m pip install csvkit
```

Basics some command and bonus tips find out the all .csv file in your current directory
```bash
find *.csv
csvstat data.csv
csvlook data.csv # cat data.csv
csvlook --max-rows 75 data.csv 
```

[Nbterm](https://github.com/davidbrochart/nbterm) or Jupyter Notebook in the terminal.

```bash
pip install nbterm
```

[Pgcli](https://github.com/dbcli/pgcli) is a command line interface for Postgres with auto-completion and syntax highlighting.

```bash
pip install pgcli
$ sudo -i -u postgres
$ pgcli
```
[Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) provides a contents manager that let Jupyter open and save notebooks as text files.

```bash
pip install jupytext
$ touch data.py
$ jupytext --to notebook data.py
$ jupyter-notebook data.ipynb 
```
After selecting the kernel in the Jupter Notebook press Ctrl + S which means save then you can use it above nbterm ways. 

## Desktop Entry Anaconda, Jupyter, Spyder
Anaconda-Navigator
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Anaconda-Navigator
GenericName=Anaconda
Comment=Scientific Python Development Environment - Python3
Exec=/home/msjahid/anaconda3/bin/anaconda-navigator
Categories=Development;Science;IDE;Qt;Education;
Icon=/home/msjahid/anaconda3/lib/python3.11/site-packages/anaconda_navigator/static/images/anaconda-icon-256x256.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```
Spyder
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Spyder
GenericName=Spyder
Comment=The Scientific Python Development Environment
Exec=/home/msjahid/anaconda3/bin/spyder
Categories=Development;Science;IDE;Qt;
Icon=/home/msjahid/anaconda3/lib/python3.11/site-packages/anaconda_navigator/static/images/spyder-icon-1024x1024.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```
Jupyter-notebook
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Jupyter-Notebook
GenericName=Notebook
Comment=Comment=Open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text.
Exec=/home/msjahid/anaconda3/bin/jupyter-notebook
Categories=Development;Science;IDE;Qt;Education;
Icon=/home/msjahid/anaconda3/lib/python3.11/site-packages/anaconda_navigator/static/images/jupyter-icon-1024x1024.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```
Jupyter Lab
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Jupyter-Lab
GenericName=JupyterLab
Comment=Comment=Open-source web-based interactive development environment for Jupyter notebooks, code, and data.
Exec=/home/msjahid/anaconda3/bin/jupyter-lab
Categories=Development;Science;IDE;Qt;Education;
Icon=/home/msjahid/anaconda3/lib/python3.11/site-packages/anaconda_navigator/static/images/jupyterlab-icon-1024x1024.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```
Ipython Console
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Jupyter QTConsole
GenericName=Interactive Python Shell
Comment=Comment=Enhanced interactive Python shell
Exec=/home/msjahid/anaconda3/bin/jupyter-qtconsole
Categories=Development;IPython;Console;Python;IDE;Development;
Icon=/home/msjahid/anaconda3/lib/python3.11/site-packages/anaconda_navigator/static/images/qtconsole-icon-1024x1024.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```

# Linux Terminal Basic Keyboard Shorcurt
```bash
ctrl + u = erase everything from the current cursor 
ctrl + k = Cuts the line after the cursor to the clipboard
ctrl + a = move the cursor to the beginning of the line
ctrl + y = common shortcut to redo an action
ctrl + shift + up arrow = move text upwise
ctrl + shift + down arrow = move text downwise
ctrl + n = New Terminal Window
ctrl + r = start the reverse-i search
ctrl + page up = Move terminal Tab
ctrl + page down = Move terminal Tab
ctrl + c = Copy text
ctrl + v = Paste Text
ctrl ++ = Zoom in
ctrl +- = Zoom out
ctrl + f = Find text
ctrl + t = Create New Terminal Tab
ctrl + n = Create New Terminal Window
ctrl + w = Close Current Terminal Tab
ctrl + shift + w = Close current Window
ctrl + l = Clears the screen
```
# Basic Shell command
```bash
rm data.py # remove single file
rm data.py data.ipynb # Delete multiple files
rm -- test.* # Remove all test files don't care about their extension
rm -rf test # Remove directory
touch data.py && jupytext --to notebook data.py # two line command using in single line you can use ; instead of && look like
# touch data.py; jupytext --to notebook data.py
# cmd1 || cmd2
$ cd myfolder || ls  # if failed cd to myfolder, `ls` will run
```
