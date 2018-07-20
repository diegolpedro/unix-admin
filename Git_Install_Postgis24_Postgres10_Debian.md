## Instalar Postgres10 y PostGIS2.4 en Debian
<p>Paso a paso para configurar postgresql y postgis en distribuciones basadas en debian. Probado solo en Ubuntu 16.04 LTS.</p>

[Info - www.ubuntuupdates.org](https://www.ubuntuupdates.org/ppa/postgresql?dist=xenial-pgdg)

#### Agrega repositorio de postgres
-----------------------------------
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" >> /etc/apt/sources.list.d/postgresql.list'
```

[Info - wiki.openstreetmap.org](https://wiki.openstreetmap.org/wiki/PostGIS/)
#### Instalamos Postgres
```
sudo apt-get -y update
sudo apt-get -y install postgresql postgresql-contrib 
```

#### Soluciona problemas de region
```
sudo dpkg-reconfigure locales
```

[Info - digitalocean.com](https://www.digitalocean.com/community/tutorials/como-instalar-y-utilizar-postgresql-en-ubuntu-16-04-es)
#### Modificar "pg_hba.conf"
```
sudo vim /etc/postgresql/10/main/pg_hba.conf
```
Modificamos las siguientes lineas para que se vean de la siguiente forma.
```
"local" is for Unix domain socket connections only
local   all             all                                     peer
IPv4 local connections:
host    all             all             0.0.0.0/0               md5
```

#### Modificar "postgresql.conf"
```
sudo vim /etc/postgresql/10/main/postgresql.conf
```
Modificamos las siguientes lineas para que se vean de la siguiente forma. De esta manera escuchara todos los clientes.
```
listen_address='*'
```

#### Reiniciamos servicio
```
sudo /etc/init.d/postgresql restart
```

#### Creamos los usuarios en el sistema
```
sudo adduser dpedro			  # Creo usuario en el sistema.
sudo adduser dpedro sudo	# Agrego dpedro a la lista de sudoers.
```

#### Creamos dpedro en postgres
```
sudo -u postgres -i psql -c "CREATE USER dpedro;"
sudo -u postgres -i psql -c "ALTER USER dpedro WITH ENCRYPTED PASSWORD 'xxxx';"
sudo -u postgres -i psql -c "GRANT ALL PRIVILEGES ON DATABASE postgres TO dpedro;"
sudo -u postgres -i psql -c "ALTER USER dpedro WITH CREATEDB;"
```

#### Modificamos pasword de postgres
```
sudo -u postgres -i psql -c "ALTER USER postgres WITH ENCRYPTED PASSWORD 'xxxx';"
```

#### Instalamos Postgis 2.4
```
sudo apt-get install postgis postgresql-10-postgis-2.4 postgresql-10-postgis-2.4-scripts
```

#### Creo base de datos de prueba y activo postgis en prueba_db
```
sudo -u postgres createdb --encoding=UTF8 --owner=dpedro prueba_db
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION postgis;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION postgis_topology;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION postgis_sfcgal;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION fuzzystrmatch;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION address_standardizer;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION address_standardizer_data_us;"
sudo -u postgres -i psql -d prueba_db -c "CREATE EXTENSION postgis_tiger_geocoder;"
```
