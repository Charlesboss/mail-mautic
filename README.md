# mail-mautic
Repositório de email do Mautic
Arquivos de Criação da aplição de codigo aberto do Mautic

##################################################################
######                 Install Mautic
##################################################################

mysql -u root
CREATE DATABASE mautic2;
CREATE USER 'mautic'@'localhost' IDENTIFIED BY 'Teste1234';
GRANT ALL PRIVILEGES ON mautic.* TO 'mautic'@'localhost';
FLUSH PRIVILEGES;
exit






##################################################################
###### Temos Que criar uma nova pasta para 
###### Instalação do Mautic
##################################################################

mkdir /var/www/html/mautic/




##################################################################
###### Baixar a Ultima Versão do Git
##################################################################


wget https://github.com/mautic/mautic/releases/download/4.3.1/4.3.1.zip && unzip 4.3.1.zip -d /var/www/html/mautic && rm 4.3.1.zip

wget https://github.com/mautic/mautic/releases/download/4.4.8/4.4.8.zip && unzip 4.4.8.zip -d /var/www/html/mautic && rm 4.4.8.zip

https://github.com/mautic/mautic/releases/download/4.4.8/4.4.8.zip
wget https://github.com/mautic/mautic/releases/download/4.4.9/4.4.9.zip && unzip 4.4.9.zip -d /var/www/html/mautic && rm 4.4.9.zip

##################################################################
###### Crie o arquivo de hosts virtuais para informar ao servidor
###### apache onde seu Mautic está localizado e onde colocar o tráfego.
###### Aqui usamos "nano" como editor:
##################################################################


nano /etc/apache2/sites-available/mautic.conf

##################################################################
###### Inserir o o arquivo
##################################################################


<VirtualHost *:80>
    ServerAdmin marcos@decodificandoamatematica.com.br
    DocumentRoot /var/www/html/mautic/
    ServerName m.decodificandoamatematica.com.br

    <Directory /var/www/html/mautic/>
    Options +FollowSymlinks
    AllowOverride All
    Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

##################################################################
###### Enable the new website on the server and restart apache
##################################################################

a2ensite mautic.conf && systemctl restart apache2

##################################################################
###### Enable the new website on the server and restart apache
##################################################################

certbot --apache --agree-tos --email marcos@decodificandoamatematica.com.br --redirect --hsts -d m.decodificandoamatematica.com.br


##################################################################
###### Last thing to do is, to give read and write permissions to the apache user (www-data):
##################################################################


chown -R www-data:www-data /var/www/html/mautic
chmod -R 755 /var/www/html/mautic
