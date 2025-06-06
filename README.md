# Mis recursos app

Se necesita crear una aplicación web que permita a los usuarios llevar un registro de su progreso al ver series, películas y leer libros. Los usuarios podrán añadir, modificar y eliminar registros de sus recursos. Y se requiere que usted diseñe las colecciones y documentos para crear una base de datos en MongoDB que soporte las funcionalidades descritas a continuación:

# **Funcionalidades Requeridas:**

## **CRUD (Crear, Leer, Actualizar, Eliminar):**

- **Crear:** Permitir al usuario añadir un nuevo recurso con los siguientes campos:
    - Nombre del recurso.
    - Género.
    - Plataforma (Ej. Netflix, Amazon, HBO, Kindle, etc.).
    - Estado (En progreso, Terminado, Pendiente).
    - Formato (Serie, Película, Libro).
    - Fecha de terminación.
    - Valoración final (1 a 5 estrellas).
    - Reseña personal (comentarios sobre el recurso).
- **Leer:** Mostrar una lista de todos los recursos almacenados con la información relevante.
- **Actualizar:** Permitir al usuario modificar los detalles de un recurso existente.
- **Eliminar:** Permitir al usuario eliminar un recurso.

## Respuesta: 

La funcionalidad **Crear** 
    
        db.contenido.insertOne({
        nombre_recurso: "Casa de Papel",
        genero: "Accion",
        plataforma: "Netflix",
        estado: "Terminado",
        tipo: "Serie",
        fecha_terminacion: ISODate("2025-06-05"),
        valoracion: "5 estrellas",
        reseña: "Muy buena y entretenida la recomiendo"
        })

        db.recursos.insertMany([{},{},{}])

La funcionalidad **Leer**

        db.recursos.find()

La funcionalidad **Actualizar**

        db.recursos.updateOne(
        { nombre_recurso: "Casa de Papel" },
        { $set: { estado: "Pendiente", fecha_terminacion: null, valoracion: null,  reseña: null } }
        )

La funcionalidad **Eliminar**

        db.recursos.deleteOne({ nombre_recurso: "Casa de Papel" })


## **Filtros y Búsqueda:**

- Implementar un sistema de filtros para que el usuario pueda ver sus recursos por:
    - Estado (Ej. Terminado, En progreso, Pendiente).
    - Formato (Ej. Serie, Película, Libro).
    - Plataforma (Ej. Netflix, Amazon, etc.).
- Incluir una barra de búsqueda para encontrar un recurso por su nombre.

# Respuesta: 

Esta sección muestra cómo realizar consultas específicas a la colección recursos para permitir filtros y búsquedas en la aplicación.

🔸 Buscar por estado:

        db.recursos.find({ estado: "Terminado" })

🔸 Buscar por formato:

        db.recursos.find({ formato: "Libro" })

🔸 Buscar por plataforma:

        db.recursos.find({ plataforma: "Netflix" })

🔸 Buscar por nombre del recurso (similar a una barra de búsqueda en frontend)

        db.recursos.find({ nombre_recurso: { $regex: "witcher", $options: "i" } })

📝 Esta búsqueda es insensible a mayúsculas/minúsculas gracias a la opción "i" y encuentra coincidencias parciales con el nombre del recurso.

## **Validación de Datos (No aplica):**

- Implementar validaciones básicas para asegurar que los datos ingresados sean correctos (Ej. Fecha de terminación debe ser una fecha válida, la valoración debe estar entre 1 y 5 estrellas, etc.).

# Entrega 5 de junio de 2025 11:59 p.m.

Se debe entregar un repositorio en GitHub con:

- Descripción del repositorio, generalidades e indicaciones en el Readme.
- Los comandos de creación de base de datos y colecciones en el Readme.
- Archivos json con el contenido de las colecciones al menos 50 registros por colección e indicando en el Readme cuales archivos json son para cada colección.