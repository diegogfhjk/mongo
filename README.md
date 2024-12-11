# Gestión de Base de Datos NoSQL con MongoDB

Este documento tiene como fin orientar sobre las operaciones que se pueden ejecutar en la base de datos para la gestion de productividad en las empresas de confeccion

## **Iniciar sesión en MongoDB**
```bash
mongosh --username root --password example
```

## **Crear la base de datos**
```bash
use prodsoft
```

## **Crear las colecciones**
```bash
db.createCollection("empleados")
db.createCollection("sensores")
db.createCollection("datos_produccion")
db.createCollection("alertas")
db.createCollection("estadisticas_historicas")
```

## **Listar colecciones**
```bash
show collections
```

## **Operaciones para las colecciones**

## **Empleados**

### Agregar datos
```bash
db.empleados.insertMany([
    {
      "id_empleado": "E001",
      "nombre": "Juan Pérez",
      "linea_produccion": "Línea 1",
      "turno": "Diurno",
      "rol": "Operario",
      "meta_unidades": 50
    },
    {
      "id_empleado": "E002",
      "nombre": "María Gómez",
      "linea_produccion": "Línea 2",
      "turno": "Nocturno",
      "rol": "Supervisor",
      "meta_unidades": 30
    }
])
```

### **Listar todos los empleados**
```bash
db.empleados.find()
```

### **Listar por nombre**
```bash
db.empleados.find({"nombre":"Juan Pérez"})
```
### **Modificar empleado**
```bash
db.empleados.updateOne(
    {"nombre":"Juan Pérez"},
    { $set: { "linea_produccion": "Linea 2" } }
)
```

### **Eliminar empleado**
```bash
db.empleados.deleteOne({"nombre":"Juan Pérez"})
```

## **Sensores**

### Agregar datos
```bash
db.sensores.insertMany([
    {
        "id_sensor": "S001",
        "ubicacion": "Máquina 3",
        "tipo_dato": "Unidades_producidas",
        "estado": "Activo"
    },
    {
        "id_sensor": "S002",
        "ubicacion": "Máquina 1",
        "tipo_dato": "Tiempo_inactividad",
        "estado": "Inactivo"
    }
])
```

### **Listar todos los sensores**
```bash
db.sensores.find()
```

### **Listar por estado**
```bash
db.sensores.find({"estado": "Activo"})
```
### **Modificar sensor**
```bash
db.sensores.updateOne(
    {"id_sensor": "S002"},
    { $set: { "estado": "Activo" } }
)
```

### **Eliminar sensor**
```bash
db.sensores.deleteOne({"id_sensor": "S001"})
```

## **Datos de produccion**

### Agregar datos
```bash
db.datos_produccion.insertMany([
    {
        "id_empleado": "E001",
        "id_sensor": "S001",
        "fecha_hora": ISODate("2024-11-15T10:30:00Z"),
        "unidades_producidas": 5
    },
    {
        "id_empleado": "E002",
        "id_sensor": "S002",
        "fecha_hora": ISODate("2024-11-15T10:35:00Z"),
        "unidades_producidas": 3
    }
])
```

### **Listar todos los datos de produccion**
```bash
db.datos_produccion.find()
```

### **Listar datos de un empleado**
```bash
db.datos_produccion.find({"id_empleado": "E001"})
```
### **Modificar datos de produccion**
```bash
db.datos_produccion.updateOne(
    {"id_empleado": "E001", "id_sensor": "S001"},
    { $set: { "unidades_producidas": 10 } }
)
```

### **Eliminar datos de produccion**
```bash
db.datos_produccion.deleteOne({"id_empleado": "E002", "id_sensor": "S002"})
```

## **Alertas**

### Agregar datos
```bash
db.alertas.insertMany([
    {
        "id_alerta": "A001",
        "fecha_hora": ISODate("2024-11-15T12:00:00Z"),
        "tipo_alerta": "Baja productividad",
        "id_empleado": "E001",
        "descripcion": "Producción por debajo del 50% esperado en la última hora"
    },
    {
        "id_alerta": "A002",
        "fecha_hora": ISODate("2024-11-15T12:10:00Z"),
        "tipo_alerta": "Falla en sensor",
        "id_sensor": "S002",
        "descripcion": "Sensor inactivo durante 5 minutos consecutivos"
    }
])
```

### **Listar todas las alertas**
```bash
db.alertas.find()
```

### **Listar alertas por tipo**
```bash
db.alertas.find({"tipo_alerta": "Baja productividad"})
```
### **Modificar alerta**
```bash
db.alertas.updateOne(
    {"id_alerta": "A001"},
    { $set: { "descripcion": "Producción menor al 40% esperado" } }
)
```

### **Eliminar alerta**
```bash
db.alertas.deleteOne({"id_alerta": "A002"})
```

## **Estadisticas historicas**

### Agregar datos
```bash
db.estadisticas_historicas.insertMany([
    {
        "id_empleado": "E001",
        "fecha": ISODate("2024-11-14T00:00:00Z"),
        "unidades_totales": 150,
        "tiempo_inactivo": "01:30:00",
        "eficiencia": 75
    },
    {
        "id_empleado": "E002",
        "fecha": ISODate("2024-11-14T00:00:00Z"),
        "unidades_totales": 120,
        "tiempo_inactivo": "01:00:00",
        "eficiencia": 80
    }
])
```

### **Listar todas las estadisticas**
```bash
db.estadisticas_historicas.find()
```

### **Listar estadisticas de un empleado en especifico**
```bash
db.estadisticas_historicas.find({"id_empleado": "E001"})
```

### **Modificar estadisticas**
```bash
db.estadisticas_historicas.updateOne(
    {"id_empleado": "E001"},
    { $set: { "eficiencia": 80 } }
)
```

### **Eliminar estadisticas historicas**
```bash
db.estadisticas_historicas.deleteOne({"id_empleado": "E002"})
```

# **Comandos de replicacion**

## Para iniciar la instancia en tipo replica
```bash
mongod --port 27017 --dbpath ~/data/n1 --replSet rs0
```

## Conexion al mongo
```bash
mongosh —port 27017
```

## Iniciar el replica set
```bash
rs.initiate({
     _id: "rs0",
     members: [
         { _id: 0, host: "localhost:27017" }
     ]
 })
```

## Ver configuracion del replica set
```bash
rs.conf()
```

## Ver status del replica set
```bash
rs.status()
```

## Agregar nodos secundarios
```bash
mongod --port 27018 --dbpath ~/data/n2 --replSet rs0
mongod --port 27019 --dbpath ~/data/n3 --replSet rs0
```

## Desde la consola principal agregar los nodos al replica set
```bash
rs.add("localhost:27018")
rs.add("localhost:27019")
```

## Eliminar nodo 
```bash
rs.remove("localhost:27019")
```

## Bajar el nodo principal
```bash
rs.stepDo\
```

## ¿El nodo es primario?
```bash
rs.isMaster()
```

# **Comandos de sharding**

## **Creacion directorios de almacenamiento de los shards**
```bash
mkdir -p ~/data/shard1/data1
mkdir -p ~/data/shard1/data2
mkdir -p ~/data/shard1/data3

mkdir -p ~/data/shard2/data1
mkdir -p ~/data/shard2/data2
mkdir -p ~/data/shard2/data3
```

## **Iniciar instancias de los shards**
```bash
mongod --shardsvr --port 26017 --dbpath ~/data/shard1/data1 --replSet shard1_replset
mongod --shardsvr --port 26117 --dbpath ~/data/shard1/data2 --replSet shard1_replset
mongod --shardsvr --port 26217 --dbpath ~/data/shard1/data3 --replSet shard1_replset
mongod --shardsvr --port 28017 --dbpath ~/data/shard2/data1 --replSet shard2_replset
mongod --shardsvr --port 28117 --dbpath ~/data/shard2/data2 --replSet shard2_replset
mongod --shardsvr --port 28217 --dbpath ~/data/shard2/data3 --replSet shard2_replset
```

## **Conexion a fragmento**
```bash 
mongosh localhost:26017
```

## **Iniciar replicaset**
```bash
rs.initiate({_id:"shard1_replset",members:[{_id:0,host:"localhost:26017"},{_id:1,host:"localhost:26117"},{_id:2,host:"localhost:26217"}]})
```

## **Conexion al otro fragmento**
```bash
mongosh localhost:28017
```

## **Iniciar replicaset**
```bash
rs.initiate({_id:"shard2_replset",members:[{_id:0,host:"localhost:28017"},{_id:1,host:"localhost:28117"},{_id:2,host:"localhost:28217"}]})
```

## **Creacion carpetas servidores de configuracion**
```bash
mkdir -p ~/data/config_server/data1
mkdir -p ~/data/config_server/data2
mkdir -p ~/data/config_server/data3
```

## **Iniciar servidores de configuracion**
```bash
mongod --configsvr --port 47017 --dbpath ~/data/config_server/data1 --replSet configserver1_replset
mongod --configsvr --port 47117 --dbpath ~/data/config_server/data2 --replSet configserver1_replset
mongod --configsvr --port 47217 --dbpath ~/data/config_server/data3 --replSet configserver1_replset
```

## **Entrar al servidor para iniciar la replicacion**
```bash
mongosh localhost:47017
```

## **Iniciar mongos**
```bash
mongos --configdb configserver1_replset/localhost:47017,localhost:47117,localhost:47217 --port 1000
```

## **Conexion al enrutador**
```bash
mongosh localhost:1000
```

## **Agregar los servidores de fragmentacion**
```bash
sh.addShard("shard1_replset/localhost:26017,localhost:26117,localhost:26217")
sh.addShard("shard2_replset/localhost:28017,localhost:28117,localhost:28217")
```

## **Habilitar la fragmentacion para la base de datos**
```bash
sh.enableSharding("prodsoft")
```

## **Habilitar fragmentacion para una colleccion**
```bash
sh.shardCollection("prodsoft.empleados", { "linea_produccion": 1 })
```

## **Agregar datos a la coleccion**
```bash
use productividadDB;

for (var i = 0; i < 10000; i++) {
    db.empleados.insertOne({
        id_empleado: "E" + (Math.floor(Math.random() * 10000) + 1).toString().padStart(5, '0'),
        nombre: "Empleado_" + (Math.floor(Math.random() * 10000) + 1),
        linea_produccion: "Línea " + (Math.floor(Math.random() * 10) + 1),
        turno: ["Diurno", "Nocturno"][Math.floor(Math.random() * 2)],
        rol: ["Operario", "Supervisor", "Técnico", "Administrativo"][
            Math.floor(Math.random() * 4)
        ], 
        meta_unidades: Math.floor(Math.random() * 100) + 20 
    });
}
```

## **Contar y verificar la distribucion de los shards**
```bash
db.empleados.count()
```

# **Comando para verificar el status del shard**
```bash
sh.status()
```