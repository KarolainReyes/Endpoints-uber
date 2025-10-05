# 🚘 Endpoints-uber

Propuesta de API para una aplicación de transportes, con un sistema similar a Uber que permite conectar usuarios y conductores, permite gestionar solicitudes de viajes, procesar pagos, registrar calificaciones y administrar la plataforma.

## ⚓ Elementos clave 
* Usuarios          
* Viajes
* Pagos
* Calificaciones

## 🪁 Preguntas de reflexión

🔹 **¿Qué entiendes por “endpoint” en el contexto de una API?**
 
  Es el punto final donde una aplicación hace solicitudes o las recibe para su manipulación o lectura.

🔹 **¿Cuál es la diferencia entre un endpoint público y uno privado?**

  Las Endpoint públicas son más recomendables para el uso de datos públicos debido a que su acceso, también es público. El uso de estas es principalmente recomendado para aplicaciones grandes o servicios con amplia accesibilidad. 

  Por otro lado, las Endpoints privadas generalmente son utilizadas para datos más sensibles. Pueden encontrarse en redes internas de organizaciones.

🔹 **¿Qué información de un usuario consideras confidencial y no debería exponerse?**

 Datos sensibles tales como documento, métodos de pago, cuentas, contraseñas, historiales de viajes, ubicación, entre otros. 

🔹 **¿Por qué es importante definir bien los métodos HTTP (GET, POST, PUT/PATCH, DELETE) en cada endpoint?**

  Es importante definir estos métodos de forma clara en cada Endpoint ya que mejoran la claridad y la especificidad de dicho Endpoint, a su vez mejora la documentación al estar mejor definidas sus funciones.

🔹 **¿Qué tipo de información requiere autenticación en este sistema?**

 En primer lugar se requiere la autenticación de inicio de sesión para los tres tipos de usuario que pertenecen a la aplicación, también para la disponibilidad de vehículos, saldo disponible en cuenta y finalización del viaje, entre otros.

🔹 **¿Cómo manejarías la seguridad de la ubicación de conductores y pasajeros?**
  
  Utilizando autenticación para verificar quien es el usuario, la autorización para determinar qué puede hacer y un cifrado (HTTPS) para proteger datos del tránsito.

🔹 **¿Qué pasaría si un viaje es solicitado y no hay conductores disponibles? ¿Cómo debería responder la API?**

El API en el Endpoint de la solicitud del viaje, en caso de no tener conductores disponibles debería tener la respuesta al usuario dentro de su body indicandole la falta de disponibilidad de conductores.

🔹 **¿Cómo identificarías los recursos principales de esta aplicación?**

Serán la entidades de nuestra aplicación, tomaremos en consideración los requisitos funcionales.
Identificamos las necesidades y fucionamientos de nuestra aplicación para poder plantear cuales serán los actores que harán parte de esta y como será su relacionamiento. 

 * Usuarios
 * Conductores
 * Vehículos
 * Viajes
 * Pagos
 * Locaciones
 * Calificaciones
 * Autenticación

🔹 **¿Qué ventajas tendría versionar la API (por ejemplo, /v1/...) desde el inicio?**

Si se requiere evolucionar en el tiempo, es necesario crear distintas versiones de la API, esto permite evolucionar de forma contolada y evitar errores.

Al versionar, también se hace más fácil el mantenimiento y soporte de la API. 

🔹 **¿Por qué es importante documentar las respuestas de error y no solo las exitosas?**

Matener un historial de los errores es clave para identificarlos y saber como reaccionar ante ellos correctamente.

Esto facilita la depuración, la documentación de errores ayuda identificar que comportamientos esperar en situaciones limitantes o inválidas. 

También ayuda a tener una lógica más clara del sistema, muestra las validaciones que existen, las reglas del negocio que se aplican y las limitantes que no deben cruzarse.

 
## 🔐 Roles y permisos

 * **Administrador** 
 * **Conductor**
 * **Pasajero**

## Recursos principales

| Recurso     | Descripción                  |
| ----------- | ---------------------------- |
| `users`     | Pasajeros y conductores      |
| `rides`     | Viajes solicitados           |
| `vehicles`  | Vehículos de los conductores |
| `locations` | Ubicación en tiempo real     |
| `payments`  | Pagos por viaje              |
| `rating`    | Calificaciones               |

## Tabla de Endpoints
| Endpoint | Método | Descripción | Autenticación | Ejemplo de cuerpo o respuesta |
|-----------|---------|--------------|----------------|-------------------------------|
| `/viajes/:id` | **DELETE** | Cancelación de viaje | Token de pasajero o conductor | `{"mensaje":"viaje cancelado exitosamente"}` |
| `/usuarios/:id` | **DELETE** | Eliminación del pasajero | Token de pasajero o administrador | `{"mensaje":"cliente eliminado exitosamente"}` |
| `/usuarios/:idconductor/calificacion` | **POST** | Calificación del conductor | Token de pasajero que tomó el viaje | `{calificacion:5,"comentario":"Carro limpio"}` |
| `/usuarios?rol=conductor&placas=HJI890` | **GET** | Buscar conductor por placas | Token de administrador | `{"mensaje":"conductor encontrado correctamente"}` |
| `/viajes/:id/asignar` | **PUT** | Tomar viaje (conductor) | Token de conductor | `{estado:"en progreso"}` |
| `/pago/:idpago/pagar` | **POST** | Pago del viaje con tarjeta | Token de pasajero, saldo disponible | `{pago:12000, estado:"completado", medio:"tarjeta"}` |
| `/usuarios` | **POST** | Creación de conductor | Público | `{nombre:"Juancho",documento:"12300",correo:"dada@gmail.com",contraseña:"12345",rol:"conductor",placas:"VDA-999"}` |
| `/viajes?fecha=2025-03-01` | **GET** | Filtrar viajes por fecha | Token de usuario | `{"mensaje":"Viaje no encontrado"}` |
| `/usuarios?rol=pasajero&calificacion_min=4&calificacion_max=5` | **GET** | Filtrar pasajeros por calificación | Token de admin o pasajero | `{"usuarios":[...]}` |
| `/usuarios/:idconductor` | **DELETE** | Eliminar conductor | Token de admin o conductor | `{"mensaje":"Usuario eliminado correctamente"}` |
| `/usuarios/:idconductor/vehiculo` | **PATCH** | Modificar vehículo del conductor | Token de conductor | `{placas:"ABC123",soat:"activo"}` |
| `/auth/login` | **POST** | Ingreso de usuario | Público | `{email:"alo123@gmail.com",contraseña:"12345"}` |
| `/usuarios/:idusuario/historial` | **GET** | Obtener historial de viajes | Token de usuario o admin | `{id:1234}` |
| `/usuarios/:iduser/ubicacion` | **GET** | Obtener ubicación de usuario | Token de pasajero o conductor | `{id:1234}` |
| `/viajes/:idviaje/mensaje` | **POST** | Enviar mensaje entre conductor y pasajero | Token de pasajero o conductor | `{mensaje:"Voy en camino",iduser:1234}` |
| `/viajes/:idviaje/finalizar` | **PATCH** | Finalizar viaje | Token de conductor | `{estado:"finalizado"}` |
| `/auth/register` | **POST** | Registro de nuevo usuario (pasajero) | Público | `{nombre:"Carlos",email:"carlos@mail.com",contraseña:"1234",rol:"pasajero"}` |
| `/vehiculos` | **GET** | Listar vehículos registrados | Token de admin | `[{"placas":"XYZ-123","estado":"activo"}]` |
| `/viajes/:id/reporte` | **POST** | Reportar incidente en el viaje | Token de pasajero o conductor | `{motivo:"Conductor llegó tarde",tipo:"retraso"}` |
| `/usuarios/:id/notificaciones` | **GET** | Consultar notificaciones del usuario | Token de usuario | `[{"mensaje":"Tu viaje ha sido asignado"}]` |


## Flujos de uso


A continuación se describen tres flujos de uso representativos de la interacción entre **cliente (pasajero o conductor)** y **servidor (API)**.

---

### 1. Solicitud, aceptación y finalización de un viaje

**Objetivo:** Representar el ciclo completo desde la solicitud de un viaje hasta su finalización por parte del conductor.

1. **Pasajero solicita un viaje**
   - **Método:** `POST /viajes`
   - **Body:** `{origen:"Calle 45 #10-23", destino:"Carrera 12 #30-18"}`
   - **Respuesta:** `{"mensaje":"Viaje creado con éxito", "id_viaje":123}`
   - **Auth:** Token del pasajero

2. **Servidor busca un conductor disponible**
   - Internamente consulta `/usuarios?rol=conductor&disponible=true`.
   - Asigna automáticamente el viaje al conductor más cercano.

3. **Conductor acepta el viaje**
   - **Método:** `PUT /viajes/123/asignar`
   - **Body:** `{estado:"en progreso"}`
   - **Respuesta:** `{"mensaje":"Viaje aceptado, en progreso"}`
   - **Auth:** Token del conductor

4. **Durante el viaje**, el conductor y pasajero pueden intercambiar mensajes:
   - **Método:** `POST /viajes/123/mensaje`
   - **Body:** `{mensaje:"Estoy cerca de tu ubicación"}`
   - **Auth:** Token de cualquiera de los dos usuarios

5. **Finalización del viaje**
   - **Método:** `PATCH /viajes/123/finalizar`
   - **Body:** `{estado:"finalizado"}`
   - **Respuesta:** `{"mensaje":"Viaje finalizado exitosamente"}`
   - **Auth:** Token del conductor

---

### 2. Cancelación de viaje y devolución parcial

**Objetivo:** Mostrar el proceso en el que un pasajero cancela un viaje y recibe un reembolso parcial.

1. **Pasajero cancela el viaje**
   - **Método:** `DELETE /viajes/123`
   - **Auth:** Token del pasajero
   - **Respuesta:** `{"mensaje":"viaje cancelado exitosamente"}`

2. **Servidor calcula penalización o devolución**
   - Lógica interna: Si el conductor ya se desplazaba, se descuenta un porcentaje.

3. **Procesar devolución**
   - **Método:** `POST /pago/321/reembolsar`
   - **Body:** `{monto:6000, estado:"devuelto"}`
   - **Auth:** Token del pasajero
   - **Respuesta:** `{"mensaje":"Reembolso procesado con éxito"}`

4. **Servidor actualiza historial de usuario**
   - Se refleja en `/usuarios/:idusuario/historial` el estado del viaje cancelado y la devolución.

---

### 3. Calificación de conductor y pasajero

**Objetivo:** Mostrar cómo se registran las calificaciones después de un viaje completado.

1. **Pasajero califica al conductor**
   - **Método:** `POST /usuarios/:idconductor/calificacion`
   - **Body:** `{calificacion:5, comentario:"Excelente servicio"}`
   - **Auth:** Token del pasajero
   - **Respuesta:** `{"mensaje":"Calificación registrada correctamente"}`

2. **Conductor califica al pasajero**
   - **Método:** `POST /usuarios/:idpasajero/calificacion`
   - **Body:** `{calificacion:4, comentario:"Buen pasajero"}`
   - **Auth:** Token del conductor
   - **Respuesta:** `{"mensaje":"Calificación del pasajero registrada"}`

3. **Servidor actualiza promedio**
   - Recalcula el puntaje promedio del usuario calificado y lo refleja en `/usuarios/:id`.

4. **Administrador puede consultar estadísticas**
   - **Método:** `GET /usuarios?rol=conductor&calificacion_min=4`
   - **Auth:** Token de administrador
   - **Respuesta:** `{"conductores_destacados":[...]}`

---

Cada flujo representa una interacción realista y coherente entre los actores del sistema, reflejando el comportamiento esperado en una plataforma de transporte tipo Uber.

## Decisiones de diseño y justificación

* Uso de API REST :

Utiliza métodos HTTP estándar (GET, PUT, POST, DELETE), es más fácil de cachar, escalar y documentar.

* Modelado de entidades 

Definimos previamente las entidades que hacen parte de nuestro aplicativo y cómo se relacionarán entre ellas.

* Autenticación y autorización

Validaciones y permisos de los usuarios

## Propuesta de mejora


## 👩‍💻 Autores


 * [Karol Reyes](https://github.com/KarolainReyes)

 * [Andres Leal](https://github.com/Andre07g)

---
