
# Manual técnico

## 1. Arquitectura

El proyecto utiliza una API desarrollada con FastAPI para clasificar mensajes de commit y almacenar los resultados en PostgreSQL.

**Componentes principales:**

- **Cliente:** navegador web o Postman, desde donde se envían las solicitudes.
- **API FastAPI:** recibe las peticiones mediante el endpoint POST /clasificar.
- **Motor eco:** clasifica los mensajes mediante reglas y expresiones regulares, sin utilizar inteligencia artificial.
- **Motor Ollama:** utiliza el modelo local gemma3:270m para clasificar los mensajes.
- **PostgreSQL:** almacena las inferencias realizadas, incluyendo el mensaje, resultado, motor y latencia.
- **Respuesta JSON:** devuelve al cliente el motor utilizado, la clasificación y el tiempo de respuesta.

**Puertos utilizados:**

| Puerto | Servicio | Función |
|---|---|---|
| 8000 | FastAPI | Recibir solicitudes de la API. |
| 5432 | PostgreSQL | Conexión con la base de datos. |
| 11434 | Ollama | Comunicación con el modelo local. |

## 2. Seguridad

**Roles de la base de datos:**

- **postgres:** usuario administrador, encargado de crear tablas, roles y administrar la base de datos.
- **app_ia:** usuario de la aplicación, tiene permisos para consultar e insertar registros en la tabla inferencias. No tiene permisos para eliminar o actualizar registros.

**Protección de credenciales:**

Las contraseñas y datos de conexión se almacenan en el archivo .env, el cual está incluido en .gitignore para evitar que se publique en GitHub.

El archivo .env.example contiene únicamente los nombres de las variables, sin información confidencial.

**Riesgos y medidas de seguridad:**

Si una contraseña se filtra, se debe cambiar inmediatamente y actualizar las credenciales de conexión. También se debe evitar publicar los puertos de la base de datos y Ollama en redes públicas.

La aplicación utiliza un usuario con permisos limitados para reducir los riesgos de acceso no autorizado.
