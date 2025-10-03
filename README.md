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

## Flujos de uso

## Desiciones de diseño y justificación

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