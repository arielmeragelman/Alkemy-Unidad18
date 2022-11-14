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



---------
Ejercitación propuesta

● Instalar MongoDB y Compass
● Acceder desde compass y crear una base de datos
● Acceder a MongoDB desde PowerShell
● Acceder a la base de datos del paso 2
● Crear dos colecciones
● Insertar 1 documentos
● Insertar varios documentos con un solo comando
● Listar los documentos existentes en una colección
● Listar un documento específico dentro de la colección
● Realizar un update en un registro
● Realizar un update a varios registros de forma simultánea


<<<< Las siguientes lineas son las salidas del shell conectado a MongoDb >>>>

-- Nos conectamos a la base de datos Prueba1 creada en el entorno de Compass
Prueba1> use Prueba1

-- Controlo todas las colecciones que hay en la base de datos
Prueba1> show collections


-- Creo Colecciones nuevas:
Prueba1> db.createCollection("Personas")
Prueba1> db.createCollection("Cursos")
Prueba1> db.createCollection("Empresas")

-- Vuelvo a controlar que las colecciones esten correctamente creadas
Prueba1> show collections
Cursos
Empresas
Personas



-- Se Insertan 2 documentos , de a uno por ejecución
Prueba1> db.Personas.insertOne({_id:32561800,Nombre:'Juan Carlos',Apellido:'Rosales',Edad:21,Ciudad:'Rio Cuarto',Situacion:'Empleado',Empresa:'Prisma SA'})
{ acknowledged: true, insertedId: 32561800 }
Prueba1> db.Personas.insertOne({ _id: 32461801, Nombre: 'Mirta Julia', Apellido: 'Quiroga', Edad: 21, Ciudad: 'Alta Gracia', Situacion: 'Empleado', Empresa: 'Prisma SA' })
{ acknowledged: true, insertedId: 32461801 }


-- Se Insertan varios documentos , todos en una misma ejecución
Prueba1> db.Personas.insertMany([{ _id: 32431821, Nombre: 'Soledad Alejandra', Apellido: 'Quiroga', Edad: 23, Ciudad: 'Alta Gracia', Situacion: 'Empleado', Empresa: 'Prisma SA' },{ _id: 32330821, Nombre: 'Silvia Ariana', Apellido: 'Salvador', Edad: 23, Ciudad: 'Rosario', Situacion: 'Empleado', Empresa: 'Alkemy' },{ _id: 31431721, Nombre: 'Alejandro Lucas', Apellido: 'Artemis', Edad: 43, Ciudad: 'Cordoba', Situacion: 'Estudiante', Empresa: 'UTN Cordoba' }])
{
  acknowledged: true,
  insertedIds: { '0': 32431821, '1': 32330821, '2': 31431721 }
}

-- Listamos todos los documentos en la colección Personas
Prueba1> db.Personas.find({})
[
  {
    _id: 32561800,
    Nombre: 'Juan Carlos',
    Apellido: 'Rosales',
    Edad: 21,
    Ciudad: 'Rio Cuarto',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32461801,
    Nombre: 'Mirta Julia',
    Apellido: 'Quiroga',
    Edad: 21,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32431821,
    Nombre: 'Soledad Alejandra',
    Apellido: 'Quiroga',
    Edad: 23,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Rosario',
    Situacion: 'Empleado',
    Empresa: 'Alkemy'
  },
  {
    _id: 31431721,
    Nombre: 'Alejandro Lucas',
    Apellido: 'Artemis',
    Edad: 43,
    Ciudad: 'Cordoba',
    Situacion: 'Estudiante',
    Empresa: 'UTN Cordoba'
  }
]
Prueba1> 

-- Listamos un documento especifico en la colección Personas a partir de su identificador
Prueba1> db.Personas.find({_id:32461801})
[
  {
    _id: 32461801,
    Nombre: 'Mirta Julia',
    Apellido: 'Quiroga',
    Edad: 21,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  }
]

-- Listamos los documentos de la colección Personas que existan con un identificador dentro de los listados

Prueba1> db.Personas.find({_id:{$in:[32330821,32431821]}})
[
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Rosario',
    Situacion: 'Empleado',
    Empresa: 'Alkemy'
  },
  {
    _id: 32431821,
    Nombre: 'Soledad Alejandra',
    Apellido: 'Quiroga',
    Edad: 23,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  }
]

-- Listamos los documentos de la colección Personas que existan con un identificador dentro de los listados y cuyo nombre este dentro de los listados
Prueba1> db.Personas.find({_id:{$in:[32330821,32431823]},Nombre:{$in:['Silvia Ariana','Soledad Alejandra']}})
[
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Rosario',
    Situacion: 'Empleado',
    Empresa: 'Alkemy'
  }
]
Prueba1> 

-- Actualizamos la Empresa de uno de los documentos especificos
Prueba1> db.Personas.updateOne({_id:32330821},{$set:{Empresa:'Georgalos SA'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
Prueba1> 

-- Controlamos los documentos cuya ciudad sea Rosario o Santa Fe y podemos confirmar que el update anterior se hizo correctamente
Prueba1> db.Personas.find({Ciudad:{$in:['Rosario','Santa Fe']}})
[
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Rosario',
    Situacion: 'Empleado',
    Empresa: 'Georgalos SA'
  }
]



-- Realizamos una busqueda de documentos cuya edad sea inferio a 25
Prueba1> db.Personas.find({Edad:{$lt:25}})
[
  {
    _id: 32561800,
    Nombre: 'Juan Carlos',
    Apellido: 'Rosales',
    Edad: 21,
    Ciudad: 'Rio Cuarto',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32461801,
    Nombre: 'Mirta Julia',
    Apellido: 'Quiroga',
    Edad: 21,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32431821,
    Nombre: 'Soledad Alejandra',
    Apellido: 'Quiroga',
    Edad: 23,
    Ciudad: 'Alta Gracia',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Rosario',
    Situacion: 'Empleado',
    Empresa: 'Georgalos SA'
  }
]

-- Ejecutamos un update de todos los documentos cuya edad sea menor a 25 y modificamos su ciudad por Buenos Aires
Prueba1> db.Personas.updateMany({Edad:{$lt:25}},{$set:{Ciudad:'Buenos Aires'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}

-- Controlamos que efectivamente se modifico la ciudad en todos los documentos seleccionados
Prueba1> db.Personas.find({Edad:{$lt:25}})
[
  {
    _id: 32561800,
    Nombre: 'Juan Carlos',
    Apellido: 'Rosales',
    Edad: 21,
    Ciudad: 'Buenos Aires',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32461801,
    Nombre: 'Mirta Julia',
    Apellido: 'Quiroga',
    Edad: 21,
    Ciudad: 'Buenos Aires',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32431821,
    Nombre: 'Soledad Alejandra',
    Apellido: 'Quiroga',
    Edad: 23,
    Ciudad: 'Buenos Aires',
    Situacion: 'Empleado',
    Empresa: 'Prisma SA'
  },
  {
    _id: 32330821,
    Nombre: 'Silvia Ariana',
    Apellido: 'Salvador',
    Edad: 23,
    Ciudad: 'Buenos Aires',
    Situacion: 'Empleado',
    Empresa: 'Georgalos SA'
  }
]
Prueba1> 
