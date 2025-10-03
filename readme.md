# 🌸✨ Diseño reflexivo de endpoints (App de transporte tipo Uber) ✨🌸

## 👩‍💻 Autoras
- 🌷 Valentina Delgado
- 🌼 Camila Florez 

---

## 💭 Preguntas guía

1. **¿Qué entiendes por “endpoint” en el contexto de una API?**  
   Un endpoint de API es una ubicación digital donde una interfaz de programación de aplicaciones (API) recibe llamadas de API, también conocidas como solicitudes de API, para recursos en su servidor. Los endpoints de API son componentes de éstas y suelen adoptar la forma de URL, o localizadores uniformes de recursos.

2. **¿Cuál es la diferencia entre un endpoint público y uno privado?**  
   Un endpoint público es accesible desde Internet, mientras que un endpoint privado es accesible solo desde una red privada específica. Los endpoints públicos ofrecen acceso amplio pero menor seguridad, mientras que los privados proporcionan mayor seguridad y control del acceso a expensas de una mayor complejidad.

3. **¿Qué información de un usuario consideras confidencial y no debería exponerse?**  
   La información confidencial abarca cualquier dato que, de verse comprometido, podría provocar daños, pérdidas o acceso no autorizado. Esto incluye información personal identificable (IPI), datos financieros, propiedad intelectual, registros de salud, y otra información confidencial.

4. **¿Por qué es importante definir bien los métodos HTTP?**  
   Definir correctamente estos métodos en cada endpoint es fundamental para garantizar la claridad, coherencia y buen funcionamiento de una API. Usarlos adecuadamente mejora la mantenibilidad del código, permite aprovechar funcionalidades como el caché, refuerza la seguridad (evitando, por ejemplo, acciones destructivas con métodos inseguros), y facilita el cumplimiento de estándares REST. Además, una API bien estructurada es más fácil de escalar, documentar, probar y versionar.

5. **¿Qué tipo de información requiere autenticación en este sistema?**  
   La información que requiere autenticación en un endpoint son credenciales que validan la identidad del solicitante, como nombres de usuario y contraseñas, tokens OAuth, JSON Web Tokens (JWT) o claves de API. Cualquier endpoint que exponga información sensible, acceda a datos confidenciales o ejecute lógica de negocio debe requerir autenticación para asegurar que solo los usuarios autorizados puedan acceder a la funcionalidad y los datos de la API. 


6. **¿Cómo manejarías la seguridad de la ubicación de conductores y pasajeros?**  
   Para asegurar la ubicación en este sistema, se debe compartir el tiempo real durante el viaje entre conductor y pasajero, con acceso restringido y autenticado. La comunicación debe ser segura (HTTPS) y los datos almacenados cifrados y por tiempo limitado. La app debe pedir permisos claros y permitir revocarlos. Se implementan controles como logging, rate limiting y validación para proteger la privacidad y cumplir normativas.

7. **¿Qué pasa si no hay conductores disponibles? ¿Cómo debería responder la API?**  
   Si un viaje es solicitado y no hay conductores disponibles, la API debería responder con un mensaje claro indicando que no hay conductores cercanos en ese momento. Por ejemplo, devolver un código 200 con un cuerpo que diga: "No hay conductores disponibles cerca en este momento. Por favor, inténtalo más tarde." Esto permite que la aplicación informe adecuadamente al pasajero y maneje la situación, como sugerir reintentar después o mostrar alternativas.


8. **¿Cómo identificas los recursos principales?**  
   Los recursos principales de esta aplicación serían los objetos o entidades clave que representan la información y operaciones del sistema. En este caso, los recursos serían:

    - **Usuarios**: pasajeros, conductores y administradores, con sus datos personales, roles y estado.
    - **Viajes**: solicitudes de viaje, estados (pendiente, aceptado, en curso, cancelado, finalizado), rutas y tiempos.
    - **Pagos**: información de cobros, historial, recibos y estado de transacciones.
    - **Calificaciones**: evaluaciones que pasajeros y conductores se dan mutuamente, con comentarios y puntuaciones.
    - **Ubicación**: datos de ubicación en tiempo real o históricos asociados a viajes y usuarios.


9. **¿Qué ventajas tendría versionar la API (por ejemplo, /v1/...) desde el inicio?**  
   Versionar la API desde el inicio permite introducir cambios y mejoras sin afectar a los usuarios actuales, facilita la evolución y el mantenimiento simultáneo de varias versiones, brinda claridad en la documentación y reduce riesgos de interrupciones, garantizando estabilidad y flexibilidad a medida que la plataforma crece.


10. **¿Por qué es importante documentar las respuestas de error y no solo las exitosas?**  
   Es importante documentar las respuestas de error porque ayudan a los desarrolladores a entender qué salió mal, cómo manejar esos errores correctamente y mejorar la experiencia del usuario. Sin una buena documentación de errores, es difícil depurar, anticipar problemas o implementar flujos adecuados frente a fallos, lo que puede generar confusión, mal funcionamiento o mala experiencia en la aplicación.


---

## 👑 Roles y permisos

| Rol         | Acciones permitidas |
|-------------|---------------------|
| 👧 Pasajera  | Solicitar viajes, pagar, calificar y ver historial. |
| 🚗 Conductora | Aceptar/finalizar viajes, calificar, gestionar su vehículo. |
| 🛠️ Administradora | Supervisar la plataforma, usuarias y reportes. |

---

## 📚 Recursos principales

- `users` – Usuarios registrados  
- `auth` – Registro e inicio de sesión  
- `rides` – Viajes solicitados  
- `payments` – Pagos y reembolsos  
- `ratings` – Calificaciones y opiniones  
- `vehicles` – Vehículos de conductoras  
- `admin` – Panel administrativo

---

## 🔗 Tabla de Endpoints


| Modulo       | Endpoint                               | Metodo | 
|--------------|----------------------------------------|--------|
| Usuarios     | /usuarios/registro                     | POST   |
|              | /usuarios/login                        | POST   | 
|              | /usuarios/historial                    | GET    |
|              | /usuarios/perfil                       | PUT    |
| Conductores  | /conductores/registro                  | POST   | 
|              | /conductores/estado                    | PUT    | 
|              | /conductores/perfil                    | GET    | 
|              | /conductores/viajes/pendientes         | GET    | 
|              | /conductores/viajes/aceptar/           | POST   | 
|              | /conductores/viajes/actual             | GET    |
| Viajes       | /viajes/solicitar                      | POST   |
|              | /viajes/cancelar/                      | POST   | 
|              | /viajes/                               | GET    | 
|              | /viajes/seguimiento/                   | GET    | 
| Pagos        | /pagos/crear                           | POST   | 
|              | /pagos/historial                       | GET    | 
| Notificaciones| /notificaciones/mostrar conductor     | GET    |
|              | /notificaciones/mostar  clientes       | GET    | 
|              | /notificaciones/pagos                  | GET    | 
| Reporte      |                                        |        |
| problemas    | /reporteProblemas/reportar             | POST   | 
|              | /reporteProblemas/contactar            | GET    | 

---
## 💡 Explicacion de los endpoints

### Usuarios
1. **registro**:
   - Crear el perfil de los usuarios.
   - Necesita el nombre completo, numero de telefono, correo electronico.
   - Devuelve el perfil del usuario ya registrado.
2. **login**:
   - Iniciar sesion para un usuario ya registrado.
   - Devuelve una sesion activa para comenzar a usar la aplicacion.
3. **historial**:
   - Mostrar el historial de viajes realizados por el usuario.
   - Requiere autenticacion del usuario.
4. **pefil**:
   - Edicion de los datos del perfil.
   - Devuelve el perfil actualizado.
 
 
 ### Conductores

5. **registro**:
   - Crear el perfil de los conductores.
   - Necesita el nombre completo, numero de telefono, correo electronico, licencia de conducir.
   - Devuelve el perfil del conductor creado.
6. **estado**:
   - Cambiar el estado del conductor (disponible o no disponible para aceptar viajes)
7. **perfil**:
   - Ver el perfil completo del conductor.
   - Necesita datos personales y estado actual.
8. **viajes pendientes**:
   - Ver la lista de viajes pendientes por aceptar disponibles para el conductor.
9. **viajes aceptar**:
   - Aceptar un viaje pendiente
   - Asigna el viaje a un conductor
10. **viaje actual**:
   - Ver detalles del viaje activo asignado al conductor (si existe).

 ### Viajes

11. **solicitar**:
   - Solicitar un nuevo viaje como pasajero.
   - Proporciona la ubicacion de origen y destino.
12. **cancelar**:
   - Cancelar un viaje activo o pendiente.
   - Puede hacerlo el pasajero o el conductor.
13. **Viajes**:
   - Consultar detalles especificos de un viaje
   - Incluye estado y conductor asignado.
14. **seguimiento**:
   - Visualizar en tiempo real la ubicacion del viaje activo para seguimiento.

 ### Pagos

15. **crear**:
   - Crear un pago para un viaje completado.
   - Se necesita especificar monto y metodo de pago.
16. **historial**:
   - Cosultar el historial de los pago sque ha realizado el usuario.

 ### Notificaciones

17. **mostrar_conductor**:
   - Enviar notificaciones a conductores disponibles cuando hay nuevos viajes para aceptar.
18. **mostrar_clientes**:
   - Enviar notificaciones a clientes cuando hay conductores disponibles para atenderlos.
19. **pagos**:
   - Enviar notificaciones relacionadas con pagos realizados o pendientes.

 ### Reporte Problemas

20. **reportar**:
   - Reportar un problema o incidencia dentro de la aplicacion.
21. **contactar**:
   - Obtener los canales de contacto disponibles para soporte o atencion al cliente.

## 💫 Flujos de uso

### 1. 🚘 Solicitar y finalizar un viaje
1. La pasajera crea un viaje.
2. Una conductora acepta.
3. Se realiza y finaliza el viaje.
4. Se paga y califican mutuamente.

### 2. ❌ Cancelar y reembolsar
1. Se cancela el viaje.
2. Se evalúa si hay reembolso.
3. Se procesa devolución.

### 3. ⭐ Calificaciones
1. Tras un viaje, ambas se califican.
2. Las calificaciones son públicas.

---

## 🧩 Decisiones de diseño

- Prefijo `/v1/` para versión.
- JWT para autenticación segura.
- Roles bien definidos para proteger datos.
- Seguridad en datos sensibles.
- Manejo de errores uniforme.

---

## 🚨 Manejo de errores

### Formato estándar
```json
{
  "error": true,
  "code": 404,
  "message": "Recurso no encontrado"
}
```
--- 
## 🚨 Mejoras

Como posibles mejoras futuras para la API de RideNow se podrían incluir: un sistema avanzado de seguimiento en tiempo real usando WebSockets para que pasajeras y conductoras visualicen la ubicación actualizada del viaje sin hacer múltiples peticiones; un módulo de promociones y descuentos que permita crear, listar y aplicar códigos promocionales para incentivar el uso de la plataforma; una gestión más completa de vehículos, donde las conductoras puedan registrar múltiples vehículos, llevar historial de mantenimiento y controlar documentos obligatorios con alertas; y finalmente, una funcionalidad de chat integrado para facilitar la comunicación directa entre pasajera y conductora durante el viaje, mejorando la coordinación y experiencia de usuario.



