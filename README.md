# 1. Utiliza la imagen de Ubuntu , tag 22 y apoyandote en esta guía sigue sus instrucciones para instalar LAMP en dicho contenedor.
sudo docker pull ubuntu:22.04  
sudo docker container create --name dam_ubuntu -i -t -p 8000:80 ubuntu:22.04  
sudo docker exec -it dam_ubuntu bash *(Se puede usar también sh)*  

**Dentro del container**  
apt update  
apt update  

apt install -y apache2 apache2-utils  
apt install -y mariadb-server mariadb-client  
apt install -y php php-mysql libapache2-mod-php 
*Configuración horaria del PHP*
![PHPHora](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2016-18-04.png?raw=true)  
<br>
*(nano se necesitará también)*  
apt install nano  
nano /etc/apache2/apache2.conf  
*(Tienes que poner al final del fichero ServerName localhost)*
![apache](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2015-42-03.png?raw=true)  

service mariadb start && service apache2 start  

# 2. Utiliza esta guía para instalar wordpress en el contenedor.  
**Primero comprobar que todo funciona**  
*Apache en el navegador*  
`http://localhost:8000  `
![apacheNet](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2016-16-07.png?raw=true)  
<br>
*PHP en el navegador*  
`http://localhost:8000/info.php    `
![phpImage](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2016-17-04.png?raw=true)  
<br>
*MariaDB*

mysql_secure_installation  
*(Aquí pedirá, entre varias otras cosas, cambiar la contraseña del root)*  
![mariaDB](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2015-42-53.png?raw=true)  

**Instalación WordPress**  
(Es necesario curl)  
apt install curl   

apt install ghostscript \  
                 libapache2-mod-php \  
                 mysql-server \  
                 php \  
                 php-bcmath \  
                 php-curl \  
                 php-imagick \  
                 php-intl \  
                 php-json \  
                 php-mbstring \  
                 php-mysql \  
                 php-xml \  
                 php-zip  

# 3. Comprueba que puedes acceder a wordpress.   
``http://localhost:8000/wp-admin/setup-config.php``  
![WordPressImg](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2016-15-24.png?raw=true)  
