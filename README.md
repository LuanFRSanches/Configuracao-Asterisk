Instalação do Asterisk no CentOS

Cenário de instalação:

* CentOS 8
* Asterisk 16.x
* Dahdi 3.x
* Libpri 1.x

Após a instalação:

 yum update
 yum -y install wget vim

Desabilite o SELinux, editando o arquivo /etc/selinux/config:

vim /etc/selinux/config

SELINUX=disabled

Agora, vamos desativar o firewall:

 systemctl stop firewalld ; systemctl disable firewalld ; init 6

Agora, vamos instalar o EPEL:

 wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

 rpm -ivh epel-release-latest-7.noarch.rpm

Instalando todas as depedencias necessárias para o Asterisk funcionar corretamente:

yum install openssl-devel ncurses-devel newt-devel libxml2-devel sqlite-devel libuuid-devel git subversion libsqlite3x-devel autoconf automake libtool libedit-devel kernel-devel gcc-c++ bzip2 patch -y ; yum groupinstall 'Development Tools'

Entrando do diretório /usr/src:
 cd /usr/src/

Baixando o Dahdi:

git clone -b next git://git.asterisk.org/dahdi/linux dahdi-linux
cd dahdi-linux
make install

Instalando o libpri na versão 1.x"

 sudo dnf install libpri-devel.x86_64


Instalando o libjanssons:

cd /usr/src/ && wget www.digip.org/jansson/releases/jansson-2.11.tar.gz

tar -zxf jansson-*

cd jansson*

./configure --prefix=/usr/ && make clean && make && make install && ldconfig

Instalando o Asterisk 16

Entrando do diretório */usr/src:

 cd /usr/src/

Baixando a versão 16 do Asterisk
dnf --enablerepo=powertools install libedit-devel
yum install libuuid-devel
yum install libxml2-devel

 wget downloads.asterisk.org/pub/telephony/asterisk/asterisk-16.22.0-rc1.tar.gz
Descompactando o Asterisk:

tar zxvf asterisk*  

Entrando no diretório Asterisk:

cd asterisk* 

Compilação e instalação completa do Asterisk:

./configure &&  make menuselect && make && make install && make config

Criando exemplos de Arquvios de configurações do Asterisk em /etc/asterisk como sip.conf, extensions.conf, entre todos os outros.(comando opcional):

make samples && cd

Iniciando o Asterisk:

#systemctl restart asterisk

 systemctl enable asterisk

Entrando em modo verbose do Asterisk

 asterisk -vvvvvvr


