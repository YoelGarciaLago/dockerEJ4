# 1. Utiliza la imagen de Ubuntu , tag 22 y apoyandote en esta guía sigue sus instrucciones para instalar LAMP en dicho contenedor.
sudo docker pull ubuntu:22.04
sudo docker container create --name dam_ubuntu -i -t -p 8000:80 ubuntu:22.04
sudo docker exec -it dam_ubuntu bash

**Dentro del container**
apt update  
apt update  

apt install -y apache2 apache2-utils  
apt install -y mariadb-server mariadb-client  
apt install -y php php-mysql libapache2-mod-php 
*(nano se necesitará también)*  
apt install nano  
nano /etc/apache2/apache2.conf  
*(Tienes que poner al final del fichero ServerName localhost)*
![apache](https://github.com/YoelGarciaLago/dockerEJ4/blob/main/Captura%20de%20pantalla%20de%202024-10-25%2015-42-03.png?raw=true)

service mariadb start && service apache2 start

# 2. Utiliza esta guía para instalar wordpress en el contenedor.

# 3. Comprueba que puedes acceder a wordpress. 
