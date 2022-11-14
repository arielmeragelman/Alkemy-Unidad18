# Alkemy-Unidad18
Bases de datos no relacionales 


Las practicas parten de una imagen de MongoDB oficial
https://www.mongodb.com/compatibility/docker


Para sintetizar los pasos descargamos,instalamos y ejecutamos el contenedor con
docker run --name mongodb -d -p 27017:27017 mongo -v

· ENTORNOS DE PRUEBA
Para las consultas contra la base de dato usamos Mongo Compass que es un cliente GUI 
https://avbravo-2.gitbook.io/docker/mongodb/mongodb-compass

Tambien ejecutamos pruebas sobre shell usando mongosh
https://www.mongodb.com/docs/mongodb-shell/install/#std-label-mdb-shell-install
https://www.mongodb.com/docs/mongodb-shell/connect/#std-label-mdb-shell-connect

En el caso particular de la prueba se ejecuto la conexion usando la imagen antes indicada de MongoDB con una imagen de Docker corriendo sobre Debian 11
Para lo cual se uso el siguiente PPA para poder descargar mongosh
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/4.4 main" | tee /etc/apt/sources.list.d/mongodb-org.list

Una vez ejecutada la instalacion se puede iniciar la conexion (si dejamos los puertos configuramos como el ejemplo inicial) usando
>mongosh



