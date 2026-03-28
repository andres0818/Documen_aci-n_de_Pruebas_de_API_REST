# 🧪 Actividad: Configuración y Pruebas de Proyecto Spring Boot con Base de Datos en la Nube (Prisma.io)

**Nombre del Estudiante:** Jean Medina\
**Repositorio Fork:** https://github.com/Jcmedinah/26_b2_r1


------------------------------------------------------------------------

# 🧪 Laboratorio: Documentación de Pruebas de API REST

Este laboratorio documenta las pruebas realizadas a una API REST para la gestión de estudiantes.
Las peticiones fueron ejecutadas en un entorno local utilizando herramientas como **Postman** o **Insomnia**.

<<<<<<< HEAD
La API se ejecuta en el siguiente endpoint base:
=======

```
http://localhost:8080/api/students
```

---

# 🚀 Guía de Pruebas y Documentación

## 1. Crear un nuevo estudiante

**Método:** `POST`
**URL:**

```
http://localhost:8080/api/students
```

### Cuerpo de la Petición

```json
{
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}
```

### Respuesta del Servidor

```json
{
  "id": 1,
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}
```

**Código de Estado (Status Code):**

```
201 Created
```

---

## 2. Obtener la lista completa de estudiantes

**Método:** `GET`

**URL:**

```
http://localhost:8080/api/students
```

### Respuesta del Servidor

```json
[
  {
    "id": 1,
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "phone": "3004445566"
  }
]
```

**Código de Estado (Status Code):**

```
200 OK
```

---

## 3. Buscar estudiante por ID (Existente)

**Método:** `GET`

**URL**

```
http://localhost:8080/api/students/1
```

### Respuesta del Servidor

```json
{
  "id": 1,
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}
```

**Código de Estado (Status Code):**

```
200 OK
```

---

## 4. Buscar estudiante por Email

**Método:** `GET`

**URL**

```
http://localhost:8080/api/students/email/ana.garcia@estudiante.com
```

### Respuesta del Servidor

```json
{
  "id": 1,
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}
```

**Código de Estado (Status Code):**

```
200 OK
```

---
1. ¿Cuál es la diferencia entre los códigos de estado 200 y 201? ¿En qué endpoints se obtuvieron cada uno?

Respuesta:

El código 200 OK indica que la petición se ejecutó correctamente y que el servidor devuelve la información solicitada. Se utiliza normalmente en peticiones GET, cuando se consulta información existente.

El código 201 Created indica que la petición se ejecutó correctamente y que se creó un nuevo recurso en el servidor. Este código se usa generalmente en peticiones POST.

En el laboratorio:

201 Created se obtuvo en el endpoint POST /api/students, cuando se creó un nuevo estudiante.

200 OK se obtuvo en los endpoints GET /api/students, GET /api/students/{id} y GET /api/students/email/{email}, cuando se consultaron los estudiantes.

2. En el escenario de error (punto 6), ¿qué información devuelve la API y por qué es importante para un desarrollador frontend recibir un código 404 en lugar de un código 500?

Respuesta:

En el escenario de error, la API devuelve un código de estado 404 Not Found, lo que indica que el recurso solicitado no existe en el servidor. Generalmente también puede devolver un mensaje en formato JSON explicando que el estudiante no fue encontrado.

Es importante que el frontend reciba un 404 porque este código indica claramente que el recurso no existe. Esto permite al desarrollador frontend mostrar un mensaje adecuado al usuario, como “Estudiante no encontrado”.

En cambio, un 500 Internal Server Error indica un problema interno del servidor, lo que significa que la aplicación falló. Esto no da información útil sobre el recurso solicitado y dificulta el manejo correcto del error en la interfaz.

3. ¿Qué sucede en la base de datos PostgreSQL cuando se ejecuta con éxito la petición DELETE? (Explique brevemente en términos de persistencia).

Respuesta:

Cuando se ejecuta correctamente una petición DELETE, el registro correspondiente al estudiante es eliminado de la base de datos PostgreSQL.

Esto significa que el dato deja de existir en la tabla donde se almacenan los estudiantes, y el cambio se guarda de forma persistente, es decir, permanece eliminado incluso después de reiniciar la aplicación o el servidor.

4. Si intentara crear un estudiante con el mismo email que ya existe en la base de datos, ¿qué cree que sucedería y qué código de error sería el más adecuado para devolver?

Respuesta:

Si se intenta crear un estudiante con un email que ya existe, la base de datos probablemente generará un error de restricción de unicidad (unique constraint) si el campo email está configurado como único.

El código de estado más adecuado para devolver sería 409 Conflict, ya que indica que la petición no se pudo completar porque entra en conflicto con el estado actual del recurso.

Esto permite al frontend informar al usuario que el correo electrónico ya está registrado y debe ingresar uno diferente.

5. ¿Por qué utilizamos el método PUT para actualizar y no el método POST? ¿Cuál es la convención técnica detrás de esta decisión?

Respuesta:

El método PUT se utiliza para actualizar un recurso existente, mientras que POST se utiliza para crear nuevos recursos.

La convención en las API REST es que:

POST se usa para crear un nuevo recurso en el servidor.

PUT se usa para modificar o reemplazar un recurso que ya existe.

Además, PUT es idempotente, lo que significa que si se ejecuta varias veces con los mismos datos, el resultado será el mismo. Esto lo hace más adecuado para operaciones de actualización.