Instalação do Asterisk no CentOS

Cenário de instalação:

* CentOS 7
* Asterisk 16.x
* Dahdi 3.x
* Libpri 1.4

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

Baixando o Dahdi na versão 3:

wget downloads.asterisk.org/pub/telephony/dahdi-linux-complete/dahdi-linux-complete-3.0.0+3.0.0.tar.gz

Descompactando o Dahdi:

tar zxvf dahdi-linux-complete*

Entrando no diretório do Dahdi:

 cd dahdi-linux-complete

Instalando o Driver Dahdi:

 make && make install && make config

Instalando o libpri na versão 1.4"

 cd /usr/src/

 wget downloads.asterisk.org/pub/telephony/libpri/libpri-1.6.0.tar.gz

tar zxvf libpri*

 cd libpri*

 make && make install 

Instalando o libjanssons:

cd /usr/src/ && wget www.digip.org/jansson/releases/jansson-2.11.tar.gz

tar -zxf jansson-*

cd jansson*

./configure --prefix=/usr/ && make clean && make && make install && ldconfig

Instalando o Asterisk 16

Entrando do diretório */usr/src:

 cd /usr/src/

Baixando a versão 16.0.1 do Asterisk

 wget downloads.asterisk.org/pub/telephony/asterisk/asterisk-16.1.1.tar.gz

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


