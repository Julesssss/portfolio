---
layout: post
title: Prepare a fresh linux installation
date: 2019-07-03 11:35:00 +0100
categories: [ubuntu, linux, install-guide]
permalink: /notes/ubuntu/prepare-a-new-system
published: false
---
Steps needed to prepare a system when it was completely wiped out or is new. Commands ready to copy and paste.

## Folders to create
~~~ bash
mkdir ~/Dokumente/personal ~/Dokumente/projects ~/programs ~/tmp ~/Dokumente/projects/ncp ~/Dokumente/projects/ncp/develop ~/Dokumente/projects/ncp/feature1 ~/Dokumente/projects/ncp/feature2 ~/Dokumente/projects/ncp/feature3 ~/Dokumente/projects/ncp/feature4
~~~
<!--more-->
## Sym links
~~~ bash
ln -s ~/Dokumente/projects/ncp ~/project;
ln -s ~/Dokumente/projects ~/projects
ln -s ~/Dokumente/personal ~/personal
~~~

## Programs to install
Download, extract and move into `~/programs`
* [Rambox](https://rambox.pro/#ce)
* [Atom](https://atom.io/)
* [DBeaver](https://dbeaver.io/download/)
* [Intellij](https://www.jetbrains.com/idea/download/#section=linux)
* [Gitkraken](https://www.gitkraken.com/download)
* [Liquibase](https://download.liquibase.org/download/?frm=n)

### Shell (Terminator + Oh my ZSH)
[Oh my ZSH](https://github.com/robbyrussell/oh-my-zsh)
``` bash
# Prerequisites + Terminator
sudo apt-get install zsh fonts-powerline dconf-cli terminator
```
log-out, close session and log-in again to refresh the shell.

#### Install Oh my ZSH
``` bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

#### Change and configure Theme
Modify file `~/.zshrc` and change the variable `ZSH_THEME="robbyrussell"` for `="agnoster"`

~~~ bash
git clone git://github.com/sigurdga/gnome-terminal-colors-solarized.git ~/.solarized
cd ~/.solarized
./install.sh
~~~

After installation, edit `~/.zshrc` again and add the following line
~~~ bash
eval `dircolors ~/.dir_colors/dircolors`
~~~

Open terminator, right click on the shell > Einstellungen > Profile > Farben   
1. Vorder- und Hintergrund > Integrierte Schemata > dunkel Solarisiert  
2. Farbpalette > Integrierte Schemata > Gruvbox dunkel

#### Install zsh-autosuggestions
We only need the `zsh-autosuggestions.zsh` script.
~~~ bash
cd ~/.oh-my-zsh/custom
git clone https://github.com/zsh-users/zsh-autosuggestions.git
cp zsh-autosuggestions/zsh-autosuggestions.zsh ..
gio trash zsh-autosuggestions/
~~~

#### Reference(s)
https://github.com/robbyrussell/oh-my-zsh  
https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH  
https://gist.github.com/renshuki/3cf3de6e7f00fa7e744a  
https://github.com/zsh-users/zsh-autosuggestions

### Docker
#### CE
~~~ bash
# Prerequisites
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"    

# Docker CE
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world # verify
~~~

#### Reference(s)
https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository

#### Compose
~~~ bash
sudo apt-get install docker-compose
~~~

### Open JDK
~~~ bash
sudo apt-get install openjdk-8-jdk
~~~
Restart

### Postman
~~~ bash
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz
~~~
Extract it. Move it to desired location.

### Maven
~~~ bash
sudo apt-get install maven
~~~

Copy `settings.xml` into `~/.m2` if necessary.

### MongoDB
Create the directories `/data/db`

~~~ bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
sudo apt-get install mongodb-org
~~~

To start the service `sudo mongod &`

#### Problems
Sometimes it's tricky to get it right at the first installation. If you're getting a conflict like the following:

~~~ bash
Paketlisten werden gelesen... Fertig
Abhängigkeitsbaum wird aufgebaut.       
Statusinformationen werden eingelesen.... Fertig
Probieren Sie »apt --fix-broken install«, um dies zu korrigieren.
Die folgenden Pakete haben unerfüllte Abhängigkeiten:
 mongodb-org : Hängt ab von: mongodb-org-server soll aber nicht installiert werden
               Hängt ab von: mongodb-org-mongos soll aber nicht installiert werden
               Hängt ab von: mongodb-org-tools soll aber nicht installiert werden
E: Unerfüllte Abhängigkeiten. Versuchen Sie »apt --fix-broken install« ohne Angabe eines Pakets (oder geben Sie eine Lösung an).
~~~

and `sudo apt --fix-broken install` does nothing. Try to remove all the conflicting packages and install them again.

~~~ bash
sudo apt-get purge x # do for all installed mongo packages
sudo apt-get autoremove
sudo apt-get install -f
~~~

#### Reference(s)
https://www.howtoforge.com/tutorial/install-mongodb-on-ubuntu/

### MySQL
Use it through Docker. We use a specific MySQL version and I couldn't install it in local.

## Create desktop entries
This is to be able to start them through menu key. They're saved at cd `~/.local/share/applications`  
Example entry:
~~~ bash
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Name=IntelliJ
Path=/home/msanchez/Programs/intellij
Exec=/home/msanchez/Programs/intellij/bin/idea.sh
Icon=/home/msanchez/Programs/intellij/bin/idea.png
~~~

## Additional Steps
* Clone git repositories into `~/Dokumente/projects`
* Import them into `Gitkraken`
* Set username, password and initialize `git flow`.  

* Copy `bash_aliases` file
