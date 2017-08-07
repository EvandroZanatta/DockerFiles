# ------------
# --- LAMP ---
# ------------

FROM ubuntu:16.04

# -------------
# @@@ BEGIN @@@
# -------------

RUN apt-get update 

RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y software-properties-common python-software-properties
RUN apt-get install curl

# ----------------------
# --- INSTALL APACHE ---
# ----------------------

RUN apt-get -y install apache2

# FOR SSL https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04

# -------------------
# --- INSTALL PHP ---
# -------------------

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update

RUN apt-get -y install php7.1 libapache2-mod-php7.1 php7.1-curl

# ---------------------
# --- INSTALL MYSQL ---
# ---------------------

# password root:123456
RUN echo 'mysql-server mysql-server/root_password password 123456' | debconf-set-selections
RUN echo 'mysql-server mysql-server/root_password_again password 123456' | debconf-set-selections
RUN apt-get -y install mysql-server --no-install-recommends
RUN sed -ie "s/^bind-address\s*=\s*127\.0\.0\.1$/bind-address = 0.0.0.0/" /etc/mysql/my.cnf 

# --------------------------
# --- INSTALL PHPMYADMIN ---
# --------------------------

RUN echo 'phpmyadmin phpmyadmin/dbconfig-install boolean true' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/app-password-confirm password phpmyadmin_password ' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/mysql/admin-pass password 123456' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/mysql/app-pass password 123456' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2' | debconf-set-selections
RUN /etc/init.d/mysql start; apt-get -y install phpmyadmin --no-install-recommends

# --------------------
# --- INSTALL NODE ---
# --------------------

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y build-essential

# ---------------------
# --- INSTALL EXTRA ---
# ---------------------

RUN apt-get install git -y
RUN apt-get install mc -y
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# -----------
# @@@ END @@@
# -----------

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get autoclean -y
RUN apt-get autoremove -y

RUN service apache2 start

CMD bash
WORKDIR /var/www/html
EXPOSE 80 443

# mysqld_safe
