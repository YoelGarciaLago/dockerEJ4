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
En este enlace te pedirá diferentes datos para conectarse a la base de datos, aunque también puedes ir a esta ruta (/srv/www/wordpress/wp-config.php) y poner lo siguiente:   
``
<?php
  /**
   * The base configuration for WordPress
     *
     * The wp-config.php creation script uses this file during the installation.
     * You don't have to use the website, you can copy this file to "wp-config.php"
     * and fill in the values.
     *
     * This file contains the following configurations:
     *
  * * Database settings
  * * Secret keys
  * * Database table prefix
  * * ABSPATH
   *
     * @link https://developer.wordpress.org/advanced-administration/wordpress/wp-config/
     *
     * @package WordPress
     */
  
  // ** Database settings - You can get this info from your web host ** //
  /** The name of the database for WordPress */
  define( 'DB_NAME', 'tu_BD' );
  
  /** Database username */
  define( 'DB_USER', 'tu_usuario' );
  
  /** Database password */
  define( 'DB_PASSWORD', 'tu_contraseña' );
  
  /** Database hostname */
  define( 'DB_HOST', 'localhost' );
  
  /** Database charset to use in creating database tables. */
  define( 'DB_CHARSET', 'utf8mb4' );
  
  /** The database collate type. Don't change this if in doubt. */
  define( 'DB_COLLATE', '' );
  
  /**#@+
  * Authentication unique keys and salts.
   *
   * Change these to different unique phrases! You can generate these using
   * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
   *
   * You can change these at any point in time to invalidate all existing cookies.
   * This will force all users to have to log in again.
   *
   * @since 2.6.0
   */
  define( 'AUTH_KEY',         's[u1wXGyctU,mlo?e]@9oF8H5 2TvN{cXIW$Bka$2y1mHiewl^#wbs?5^w}bqiZV' );
  define( 'SECURE_AUTH_KEY',  '%c|p_{W18!)`0Z-;$o[0_Gw!>FcjP,lRJXi/M1[?#>o0:p[@su$]P=DIR}$BqjG(' );
  define( 'LOGGED_IN_KEY',    'G.ui.lm42ILdmyeWLg)~:rO,6o`gkUeDKq9]$7x$snYHW6!I0>A3cRK~!x ]` z<' );
  define( 'NONCE_KEY',        '[xUHnT-um:]H;X._l7p_#J!T3M`Iy]Od%%.*ImS~2_Z{?s)2t). 6GQie0,;Y!n4' );
  define( 'AUTH_SALT',        '_p7zJt7xK1O6Ap{&J,a#2{eFlCLKi*ZMw3A!1bR#WT?@srOmM$e);X<+ia]<`b?a' );
  define( 'SECURE_AUTH_SALT', '%3{{P[$)R5dLwk=uE3NcPo]`;f`ND5oO!@E.cc9`.X/Qgz719lt.0uP:UuB56CKu' );
  define( 'LOGGED_IN_SALT',   '8x&Xtei=>P#7NI@f,yGOS7-9V}LMKS/-X^UiVLzKlV8GQBv8%I[#f7^nP^~N/7N3' );
  define( 'NONCE_SALT',       'OLK3Lg|^p|&<p~{{B8@g%t/a}wXpV(R(HETQ7Y1o}YiW&@[a#%4Gs1|b*j?RoZ1.' );
  
  /**#@-*/
  
  /**
  * WordPress database table prefix.
   *
   * You can have multiple installations in one database if you give each
   * a unique prefix. Only numbers, letters, and underscores please!
   */
  $table_prefix = 'wp_';
  
  /**
  * For developers: WordPress debugging mode.
   *
   * Change this to true to enable the display of notices during development.
   * It is strongly recommended that plugin and theme developers use WP_DEBUG
   * in their development environments.
   *
   * For information on other constants that can be used for debugging,
   * visit the documentation.
   *
   * @link https://developer.wordpress.org/advanced-administration/debug/debug-wordpress/
   */
  define( 'WP_DEBUG', false );
  
  /* Add any custom values between this line and the "stop editing" line. */
  
  
  
  /* That's all, stop editing! Happy publishing. */
  
  /** Absolute path to the WordPress directory. */
  if ( ! defined( 'ABSPATH' ) ) {
    define( 'ABSPATH', __DIR__ . '/' );
  }
  
  /** Sets up WordPress vars and included files. */
  require_once ABSPATH . 'wp-settings.php';
``
