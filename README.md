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