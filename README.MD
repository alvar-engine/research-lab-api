# Fundamentos del Protocolo HTTP y su Rol en APIs Web

**Maria Loreto Vallejos - Alvaro Latorre**  
**Cohorte: [JAVA-22]**  
**Fecha: 29 de Octubre de 2025**



---

## 📘 **Índice:**

1. [Introducción](#1-introducción)  
 

2. [HTTP vs HTTPS](#2-http-vs-https)  
   - [2.1. ¿Qué es HTTP?](#21-qué-es-http)  
   - [2.2. ¿Qué es HTTPS?](#22-qué-es-https)  
   - [2.3. Cifrado SSL/TLS](#23-cifrado-ssltls)  
   - [2.4. ¿Por qué HTTPS es más seguro que HTTP?](#24-por-qué-https-es-más-seguro-que-http)  
   - [2.5. ¿Qué pasa si un sitio no usa HTTPS?](#25-qué-pasa-si-un-sitio-no-usa-https)

3. [Modelo TCP/IP y comunicación en red](#3-modelo-tcpip-y-comunicación-en-red)  
   - [3.1. Capas del modelo TCP/IP](#31-capas-del-modelo-tcpip)  
   - [3.2. Relación entre HTTP y TCP/IP](#32-relación-entre-http-y-tcpip)

4. [Puertos de comunicación](#4-puertos-de-comunicación)  
   - [4.1. ¿Qué es un puerto y por qué es importante?](#41-qué-es-un-puerto-y-por-qué-es-importante)  
   - [4.2. Puertos principales en la web](#42-puertos-principales-en-la-web)

5. [Códigos de estado HTTP](#5-códigos-de-estado-http)   
   - [5.1. Categorías de códigos HTTP](#51-categorías-de-códigos-http)  
   - [5.2. Tabla ampliada de códigos comunes](#52-tabla-ampliada-de-códigos-comunes)

6. [Métodos HTTP y su relación con CRUD](#6-métodos-http-y-su-relación-con-crud)  
   - [6.1. Principales métodos HTTP](#61-principales-métodos-http)  
   - [6.2. Otros métodos menos comunes](#62-otros-métodos-menos-comunes)

7. [APIs y REST](#7-apis-y-rest)  
   - [7.1. ¿Qué es una API?](#71-qué-es-una-api)  
   - [7.2. ¿Qué es REST?](#72-qué-es-rest)  
   - [7.3. ¿Qué es una API RESTful](#73-qué-es-una-api-restful) 
   - [7.3. Estructura de una solicitud a una API RESTful](#73-estructura-de-una-solicitud-a-una-api-restful)  
   - [7.4. Ejecución de solicitudes en distintas herramientas](#74-ejecución-de-solicitudes-en-distintas-herramientas)  
     - [7.4.1. cURL](#741-curl)  
     - [7.4.2. Postman](#742-postman)  
     - [7.4.3. Librería Requests en Python](#743-librería-requests-en-python)  
   - [7.5. Comparativa de herramientas](#75-comparativa-de-herramientas)

8. [Cabeceras HTTP (Headers)](#8-cabeceras-http-headers)  
   - [8.1. ¿Qué son las cabeceras?](#81-qué-son-las-cabeceras)  
   - [8.2. Tipos y ejemplos de headers comunes](#82-tipos-y-ejemplos-de-headers-comunes)
   - [8.3. Cabeceras comunes en API REST](#83-cabeceras-comunes-en-api-rest)

9. [Ejemplos reales con APIs](#9-ejemplos-reales-con-apis)

10. [Reflexión personal](#10-reflexión-personal)

11. [Fuentes](#11-fuentes)


---

## 1. Introducción



El presente informe analiza los **fundamentos del protocolo HTTP** y su papel en la comunicación entre clientes y servidores dentro del entorno web.  
HTTP (HyperText Transfer Protocol) constituye la base del intercambio de información en Internet, definiendo las reglas mediante las cuales un cliente (por ejemplo, un navegador o aplicación) solicita recursos y un servidor los entrega.  

A lo largo del documento se explica la evolución de HTTP hacia **HTTPS**, destacando la incorporación de mecanismos de **cifrado y seguridad** mediante los protocolos SSL/TLS.  
Asimismo, se aborda la relación entre **los métodos HTTP y las operaciones CRUD** (Create, Read, Update, Delete), esenciales en la interacción con **APIs RESTful**, las cuales permiten integrar sistemas, aplicaciones y servicios web de forma estandarizada.  

El trabajo incluye ejemplos prácticos de solicitudes y respuestas HTTP, descripción de **cabeceras (headers)**, **códigos de estado**, y la estructura de una petición a una API utilizando herramientas como **cURL, Postman y la librería Requests de Python**.  

Finalmente, se reflexiona sobre la importancia del protocolo HTTP como pilar del desarrollo web moderno, su influencia en la creación de aplicaciones escalables y seguras, y su rol en la interconexión global de datos y servicios digitales.





---



## 2. HTTP vs HTTPS


### 2.1 ¿Qué es HTTP?


**HTTP (HyperText Transfer Protocol)**, o **Protocolo de Transferencia de Hipertexto**, es un protocolo utilizado por los navegadores para comunicarse con los servidores web.  
El **hipertexto** corresponde a un tipo de texto codificado mediante un lenguaje de marcado estándar llamado **HTML (HyperText Markup Language)**.

HTTP establece un conjunto de reglas que permiten la transferencia de datos —como texto, imágenes y otros archivos multimedia— entre ordenadores a través de la **World Wide Web**.  
Cada vez que un usuario abre su navegador, utiliza **HTTP** de forma indirecta.

Se trata de un **protocolo de aplicación** empleado en sistemas de información **hipermedia distribuidos y colaborativos**.  

>  💡 **Tip histórico — El origen del HTTP y la Web**
>
> En **1989**, **Tim Berners-Lee**, científico del **CERN**, propuso un sistema para compartir información entre investigadores de forma más eficiente.  
> De esa idea nacieron los tres pilares de la web moderna:
> - 🌐 **HTTP (HyperText Transfer Protocol)** — el protocolo de comunicación entre cliente y servidor.  
> - 🧱 **HTML (HyperText Markup Language)** — el lenguaje de estructura de las páginas web.  
> - 🔗 **URL (Uniform Resource Locator)** — el sistema para localizar recursos en la red.  
>
> En **1990**, Berners-Lee logró la **primera comunicación cliente-servidor** usando HTTP, y en **1994** fundó el **W3C (World Wide Web Consortium)** en el **MIT**, organismo que aún define los estándares de la web.

<div align="center">
<img src="./images/http\Protocolo http.gif" alt="🔒 Candado HTTPS" width="600">
<br><em>Flujo de trabajo http</em>
</div>

---

### 2.2 ¿Qué es HTTPS?

**HTTPS (HyperText Transfer Protocol Secure)**, o **Protocolo de Transferencia de Hipertexto Seguro**, es una versión segura del protocolo **HTTP**.  
Combina el Protocolo de Transferencia de Hipertexto con los protocolos **SSL (Secure Sockets Layer)** o **TLS (Transport Layer Security)** para garantizar una **comunicación cifrada** y una **identificación segura** del servidor web.

<div align="center">
<img src="./images/https ssl tls\Candado ssl tls.webp" alt="🔒 Candado HTTPS" width="600">
<br><em></em>
</div>



HTTPS funciona de manera idéntica a HTTP, pero los mensajes de solicitud y respuesta se transmiten de forma **encriptada**, lo que impide que terceros accedan a información privada como contraseñas o números de tarjetas de crédito.  
Se utiliza automáticamente en cualquier dirección que comience con `https:` en lugar de `http:`.

Para su implementación, el servidor debe contar con un **certificado digital SSL/TLS** válido que lo identifique ante el navegador.  
El uso de **HTTPS** es esencial en aplicaciones y sitios web que manejan **datos personales o información sensible**.


---

### 2.3 Cifrado SSL/TLS (Secure Sockets Layer / Transport Layer Security)

> 🔒 **Tip histórico — El nacimiento de HTTPS**
>
> En **1994**, la empresa **Netscape** desarrolló el protocolo de seguridad **SSL (Secure Socket Layer)**, que dio origen a **HTTPS**, permitiendo transmitir datos cifrados entre el navegador y el servidor.  
>  
> En **1999**, SSL fue reemplazado por **TLS (Transport Layer Security)**, una versión mejorada que hoy se utiliza como **estándar de seguridad** en prácticamente todos los sitios web.


**SSL (Secure Sockets Layer)** y su sucesor **TLS (Transport Layer Security)** son protocolos de seguridad que permiten establecer **comunicaciones cifradas** y **autenticadas** entre un navegador y un servidor web.  
Gracias a este proceso, la información transmitida viaja de forma segura y no puede ser interceptada ni modificada por terceros.

---
### 🔐 Proceso de conexión segura
<div align="center">
<img src="./images/https ssl tls\Infografia https.png" alt="🔒 Candado HTTPS" width="600">
<br><em></em>
</div>




### ⚙️ Características de SSL/TLS
- Utiliza **claves públicas y privadas** para autenticar y establecer la conexión.  
- Cada sesión crea una **clave temporal** diferente, aumentando la seguridad.  
- Garantiza la **identidad del servidor** y la **integridad de los datos** mediante un **código de autenticación de mensajes (MAC)**.  
- Protege tanto los datos enviados por el usuario como las respuestas del servidor, evitando accesos o alteraciones no autorizadas.

---



### 2.4 ¿Por qué HTTPS es más seguro que HTTP?

**HTTPS (HyperText Transfer Protocol Secure)** es una versión segura de **HTTP** que utiliza los protocolos **SSL/TLS** para cifrar la comunicación entre el navegador y el servidor.  
A diferencia de HTTP, donde los datos se transmiten en texto plano, HTTPS protege la información mediante **encriptación**, **autenticación** y **verificación de integridad**.

#### 🔒 1. Cifrado de la información
En **HTTP**, los mensajes viajan en texto claro, lo que permite que terceros puedan leer o interceptar los datos.  
En **HTTPS**, toda la información se transmite de forma **cifrada** mediante **TLS/SSL**, evitando que alguien pueda acceder a contraseñas, datos personales o información financiera.  
El resultado es que un atacante solo vería una secuencia de caracteres aleatorios en lugar de texto legible.

#### 🧾 2. Autenticación del servidor
HTTPS verifica que el servidor web sea realmente quien dice ser mediante un **certificado digital** emitido por una **autoridad certificadora (CA)**.  
El navegador comprueba que el certificado sea válido y que coincida con el dominio del sitio.  
Esto impide ataques como la **suplantación de dominio**, el **secuestro de DNS** o los **ataques en ruta**, donde un atacante podría hacerse pasar por el servidor legítimo.

#### 🧩 3. Integridad de los datos
Con HTTPS, los mensajes incluyen un **código de autenticación (MAC)** que garantiza que la información no ha sido alterada durante la transmisión.  
Cualquier intento de modificar los datos sería detectado inmediatamente, asegurando que el contenido recibido es exactamente el que el servidor envió.

#### 🌐 4. Confianza y autoridad
Los navegadores muestran un **candado de seguridad** en la barra de direcciones cuando un sitio usa HTTPS, indicando a los usuarios que la conexión es segura.  
Además, los motores de búsqueda como **Google** priorizan los sitios con HTTPS en sus resultados, reforzando su **autoridad y credibilidad**.

#### ⚡ 5. Mejor rendimiento y análisis
Gracias a tecnologías como **HTTP/2**, que solo funciona sobre HTTPS, los sitios web cifrados suelen **cargar más rápido** que los que usan HTTP.  
Además, HTTPS permite un **mejor seguimiento del tráfico de referencia**, ayudando a los sistemas de análisis web a identificar con precisión las fuentes de visitas.

En resumen, **HTTPS protege la privacidad, la identidad y la integridad de los datos** en la web, ofreciendo un entorno más confiable tanto para los usuarios como para los propietarios de sitios.


<div align="center">
<img src="./images/https ssl tls\Diferencia entre http https.png" alt="🔒 Candado HTTPS" width="600">
<br><em></em>
</div>

---
### 2.5 ¿Qué pasa si un sitio no usa HTTPS?  

Cuando un sitio web no utiliza **HTTPS**, las conexiones entre el navegador y el servidor se realizan mediante **HTTP sin cifrado**, lo que significa que los datos viajan en texto plano y pueden ser interceptados o modificados fácilmente durante la transmisión.  

A continuación se detallan las principales consecuencias:

- **Los datos pueden ser interceptados:** sin cifrado, cualquier información enviada —como contraseñas, correos o números de tarjeta— puede ser capturada por atacantes a través de técnicas como *sniffing* o *man-in-the-middle*.  
- **No hay autenticación real del servidor:** el usuario no puede confirmar que está comunicándose con el sitio legítimo, lo que facilita ataques de suplantación (*phishing*).  
- **Formularios y contraseñas quedan vulnerables:** toda la información enviada desde el navegador puede ser leída o modificada por terceros antes de llegar al servidor.  
- **Advertencias visuales en los navegadores:** Chrome, Firefox y otros navegadores modernos muestran alertas (“**Sitio no seguro**”) que reducen la confianza del usuario y afectan directamente las conversiones.  
- **Impacto negativo en el SEO:** Google y otros motores de búsqueda priorizan los sitios que usan HTTPS, por lo que aquellos que no lo implementan sufren una **penalización en el ranking** y menor visibilidad orgánica.  

<div align="center">
<br><em>Ejemplo de repuesta del navegador ante un sitio riesgoso</em>
<img src="./images/https ssl tls\Sitio no seguro.jpeg" alt="🔒 Candado HTTPS" width="600">

</div>

---

## 3. Modelo TCP/IP y comunicación en red

El modelo **TCP/IP (Transmission Control Protocol / Internet Protocol)** es el conjunto de protocolos que permite la **comunicación de datos entre dispositivos en Internet**.  
Constituye la base de la arquitectura de red moderna y define cómo se transmiten, direccionan y reciben los datos entre clientes y servidores.

Toda comunicación —incluyendo las solicitudes y respuestas **HTTP**— viaja encapsulada a través de las **capas del modelo TCP/IP**, que trabajan de forma jerárquica para garantizar que los datos lleguen al destino correcto, íntegros y en orden.

<div align="center">
<br><em>Puertos TCP/IP</em>
<img src="./images/tcp ip\tcp ip.webp" alt="🔒 Candado HTTPS" width="600">

</div>


---

### 3.1 Capas del modelo TCP/IP

| **Capa** | **Protocolos principales** | **Función** |
|-----------|-----------------------------|--------------|
| **Aplicación** | HTTP, HTTPS, FTP, SMTP, DNS | Gestiona las interacciones entre aplicaciones y define cómo deben intercambiar datos. |
| **Transporte** | TCP, UDP | Garantiza la entrega fiable de los datos. TCP establece una conexión, segmenta la información y asegura que los paquetes lleguen en orden. |
| **Internet (Red)** | IP, ICMP | Determina la dirección de origen y destino mediante direcciones IP. Gestiona el enrutamiento y la entrega de paquetes entre redes. |
| **Acceso a la red (Enlace y física)** | Ethernet, Wi-Fi, ARP | Define cómo los datos se transmiten físicamente a través del medio (cables, fibra óptica o red inalámbrica). |


---

### 3.2 Relación entre HTTP y TCP/IP

```swift 
HTTP  →  TCP/IP  →  Puertos  →  HTTPS/TLS
```


El protocolo **HTTP** opera en la **capa de aplicación** del modelo TCP/IP.  
Cuando un cliente realiza una solicitud HTTP, esta atraviesa las diferentes capas de la siguiente manera:

1. **Capa de Aplicación:**  Genera la solicitud HTTP (por ejemplo, `GET /index.html`).

2. **Capa de Transporte (TCP):**  Divide la información en segmentos y garantiza que lleguen completos y en orden. Cada conexión HTTP utiliza **TCP** como protocolo base.

3. **Capa de Internet (IP):** Asigna direcciones IP de origen y destino, determinando la ruta que seguirá el paquete.

4. **Capa de Acceso a la red:** Transmite físicamente los paquetes a través del medio (Wi-Fi, Ethernet, etc.).


Cada servicio que opera sobre TCP/IP utiliza un **número de puerto** para identificar el tipo de comunicación que realiza.  

---

## 4. Puertos de comunicación

### 4.1 ¿Qué es un puerto y por qué es importante?

**Un puerto es un número** que identifica un punto de conexión dentro de una dirección IP. Sirve para distinguir diferentes servicios que se ejecutan en un mismo servidor.
En el caso de HTTP, los navegadores utilizan el puerto 80 por defecto para enviar y recibir solicitudes.


- **Puerto 80**: usado por HTTP sin cifrado.
- **Puerto 8080**: alternativa al 80, normalmente para entornos de desarrollo o pruebas.

**Ejemplo**:
http://localhost:8080 → el navegador se conecta al puerto 8080 del servidor local.




******Los puertos son esenciales porque******:  
- **Organizan y dirigen el tráfico de Internet** hacia el servicio correcto.  
- **Permiten múltiples conexiones simultáneas** en una misma dirección IP.  
- **Mejoran la seguridad y eficiencia** al filtrar y controlar qué servicios pueden recibir datos.  

 Los puertos funcionan como **“puertas digitales”** que gestionan cómo fluye la información entre aplicaciones y redes, siendo fundamentales para el funcionamiento estructurado y seguro de Internet.



### 4.2 Puertos principales en la web
| Puerto | Protocolo | Uso Principal | Tráfico |
|--------|-----------|---------------|---------|
| **80** | HTTP | Web no segura | Páginas web |
| **8080** | HTTP | Desarrollo/Pruebas | Apps locales |
| **443** | HTTPS | Web segura | APIs, e-commerce |
| **21** | FTP | Protocolo de transferencia archivos | Upload/Download |
| **22** | SSH | Acceso remoto seguro | Servidores |
| **3306** | MySQL | Bases de datos | Consultas SQL |

---

**Ejemplo:**  
Cuando accedemos a `https://www.ejemplo.com`, el navegador utiliza automáticamente el **puerto 443**, garantizando que todos los datos se transmitan de forma **encriptada y segura**.










---

## 5. Códigos de estado HTTP

<div align="center">
<br><em></em>
<img src="./images/Codigo http\Codigo estado.png" alt="🔒 Candado HTTPS" width="600">

</div>

> 

Es la respuesta HTTP que se envía a un cliente, el código de estado, que es un número de tres dígitos, va acompañado de una frase explicativa (también conocida como texto de estado) que resume el significado del código. Junto con la versión HTTP de la respuesta, estos elementos se colocan en la primera línea de la respuesta, que por ello se conoce como línea de estado.

---

### 5.1 Categorías de códigos HTTP
| Categoría | Rango | Descripción | Ejemplo |
|-----------|-------|-------------|---------|
| **1xx** Informativos | 100–199 | El servidor acusa recibo y está procesando la solicitud. | `100 Continue` |
| **2xx** Éxito | 200–299 |  El servidor ha recibido, entendido y procesado correctamente la solicitud. | `200 OK` |
| **3xx** Redirección | 300–399 | El servidor recibió la solicitud, pero hay una redirección a otro lugar.  | `301 Moved` |
| **4xx** Error Cliente | 400–499 | El error fue causado por el cliente. | `404 Not Found` |
| **5xx** Error Servidor | 500–599 | El error ocurre dentro del servidor. el cliente hizo una petición válida, pero el servidor no pudo completarla.  | `500 Internal` |


Los **códigos de estado HTTP** son fundamentales para la comunicación entre cliente y servidor, ya que permiten identificar si una solicitud fue exitosa, redirigida o fallida.  
Comprenderlos facilita el diagnóstico de errores, mejora la experiencia del usuario y optimiza la gestión del SEO y el rendimiento del sitio web.

---

<div align="center">
<br><em></em>
<img src="./images/Codigo http\http-status-classes.png" alt="🔒 Candado HTTPS" width="600">

</div>

----
> 

### 5.2 Tabla ampliada de códigos comunes

| Categoría | Código | Descripción | Ejemplo de uso |
|------------|--------|--------------|----------------|
| **1xx** Informativos | 100 | El servidor recibió la petición inicial y el cliente debe continuar. | `100 Continue` |
| | 101 | El servidor acepta cambiar de protocolo (por ejemplo, de HTTP a WebSocket). | `101 Switching Protocols` |
| | 103 | Permite al navegador precargar recursos antes de la respuesta final. | `103 Early Hints` |
| **2xx** Éxito | 200 | La solicitud fue procesada correctamente. | `200 OK` |
| | 201 | Un nuevo recurso fue creado exitosamente. | `201 Created` |
| | 204 | Solicitud exitosa, pero sin contenido que devolver. | `204 No Content` |
| | 206 | Solo se entrega una parte del recurso solicitado. | `206 Partial Content` |
| **3xx** Redirección | 301 | El recurso se ha movido permanentemente a una nueva URL. | `301 Moved Permanently` |
| | 302 | El recurso fue movido temporalmente. | `302 Found` |
| | 304 | El recurso no ha cambiado; se puede usar la versión en caché. | `304 Not Modified` |
| | 308 | Redirección permanente sin cambiar el método HTTP. | `308 Permanent Redirect` |
| **4xx** Error del cliente | 400 | Petición incorrecta o malformada. | `400 Bad Request` |
| | 401 | Requiere autenticación para acceder al recurso. | `401 Unauthorized` |
| | 403 | Acceso prohibido, incluso con autenticación. | `403 Forbidden` |
| | 404 | El recurso solicitado no fue encontrado. | `404 Not Found` |
| | 429 | Demasiadas peticiones en un corto tiempo. | `429 Too Many Requests` |
| **5xx** Error del servidor | 500 | Error interno; el servidor no puede procesar la solicitud. | `500 Internal Server Error` |
| | 502 | El servidor actuó como puerta de enlace y recibió una respuesta no válida. | `502 Bad Gateway` |
| | 503 | El servicio está temporalmente fuera de línea o en mantenimiento. | `503 Service Unavailable` |
| | 504 | El tiempo de respuesta del servidor o proxy se agotó. | `504 Gateway Timeout` |
| | 511 | Autenticación de red requerida para continuar. | `511 Network Authentication Required` |

<!-- - Luego, profundiza **por qué debemos conocer y reconocer especialmente estos tres códigos:**
    - `200 OK` → cuando todo sale bien.
    - `404 Not Found` → cuando el recurso no existe o fue movido.
    - `500 Internal Server Error` → cuando el problema está en el servidor.

> 💬 Explica con tus palabras cómo podrías usar estos códigos para diagnosticar errores en una API o en un proyecto web.
> -->


---




## 6. Métodos HTTP y su relación con CRUD

Los **métodos HTTP** son acciones que indican al servidor qué operación realizar sobre un recurso identificado por una URL.
Cada método expresa una intención distinta: obtener, crear, actualizar o eliminar información.

En el contexto de las **APIs REST**, estas operaciones se alinean con el modelo **CRUD**, formando la base de la comunicación entre **clientes** (como navegadores o aplicaciones) y **servidores web** en las **APIs RESTful**.

<div align="center">
<br><em></em>
<img src="./images/Metodos http\CRUD.jpeg" alt="🔒 Candado HTTPS" width="600">

</div>

### 6.1 Principales métodos HTTP

| **Acción CRUD** | **Método HTTP** | **Descripción** | **Ejemplo** |
|------------------|-----------------|-----------------|--------------|
| **Create (Crear)** | `POST` | Envía datos al servidor para crear un nuevo recurso. | `POST /api/usuarios` |
| **Read (Leer)** | `GET` | Obtiene información de un recurso sin modificarlo. | `GET /api/usuarios` |
| **Update (Actualizar)** | `PUT / PATCH` | Modifica un recurso existente. `PUT` reemplaza completamente, `PATCH` actualiza parcialmente. | `PUT /api/usuarios/3` |
| **Delete (Eliminar)** | `DELETE` | Borra un recurso identificado en la URL. | `DELETE /api/usuarios/3` |


### 6.2 Otros métodos menos comunes
| **Método HTTP** | **Descripción** | **Ejemplo** |
|------------------|-----------------|--------------|
| **PATCH** | Actualiza solo una parte del recurso existente. | `PATCH /api/usuarios/3` |
| **HEAD** | Igual que `GET`, pero solo obtiene los encabezados de la respuesta (sin el cuerpo). | `HEAD /api/usuarios` |
| **OPTIONS** | Indica qué métodos HTTP están permitidos para una URL específica. | `OPTIONS /api/usuarios` |

---
## 7. APIs y REST

### 7.1 ¿Qué es una API?

Una **API** (***Application Programming Interface***) es un conjunto de reglas y protocolos que permite que dos sistemas de software se comuniquen entre sí.
Actúa como un puente entre aplicaciones, definiendo cómo deben intercambiar datos o ejecutar funciones.

🧠 Ejemplo:
Una app de clima puede usar una API para obtener datos meteorológicos desde un servidor remoto sin necesidad de que ambos sistemas compartan la misma estructura interna.

### 7.2 ¿Qué es REST? 
**REST** (***Representational State Transfer***) es un estilo arquitectónico que define cómo deben comunicarse los sistemas a través de la web.
Se basa en principios como la interfaz uniforme, la ausencia de estado, la caché, y la arquitectura en capas, garantizando comunicación **ligera, eficiente y escalable**.

Las APIs que implementan estos principios se denominan **API REST** o **API RESTful**.
En ellas, los **recursos** (datos o servicios) se identifican mediante **URLs** y se manipulan a través de métodos HTTP estándar como GET, POST, PUT y DELETE.


<div align="center">
<br><em></em>
<img src="./images/api\restAPI.png" alt="🔒 Candado HTTPS" width="600">

</div>



### 7.3 ¿Qué es una API RESTful?

Una **API RESTful** es una interfaz que permite el intercambio de información entre sistemas mediante solicitudes HTTP directamente desde la terminal.
Cada solicitud incluye:

- Un **endpoint (URL)** que identifica el recurso.

- Un **método HTTP** que indica la acción a realizar.

- Opcionalmente, **encabezados**, **parámetros y cuerpo (payload)** con datos o autenticación.

Las **API RESTful** son ampliamente usadas porque son:

- **Escalables**: no mantienen estado entre solicitudes.

- **Flexibles**: cliente y servidor evolucionan de forma independiente.

- **Seguras**: permiten autenticación mediante tokens, claves o protocolos como OAuth y HTTPS.

- **Eficientes**: soportan almacenamiento en caché para mejorar rendimiento.
---
### 7.4 Ejecución de solicitudes en distintas herramientas

En una **API REST**, las peticiones HTTP permiten que un cliente (como una app, navegador o script) se comunique con un servidor para **crear, leer, actualizar o eliminar datos (CRUD)**.
Estas operaciones se realizan **mediante métodos HTTP** como **GET, POST, PUT, PATCH o DELETE.**

A continuación, se muestra cómo se ejecutan con tres herramientas comunes:

---

#### 7.4.1 cURL

**cURL** (*Client URL*) es una herramienta de terminal que permite enviar peticiones HTTP directamente. Es ideal para pruebas rápidas y depuración técnica.

📌  **Cómo funciona:** 

- Envía peticiones al servidor con -X (método), -H (cabeceras) y -d (datos).

- Muestra la respuesta completa: código de estado, cabeceras y cuerpo (JSON, HTML, texto, etc.).



📘 **Ejemplo GET – Leer un usuario**
```bash
curl -X GET https://jsonplaceholder.typicode.com/users/1
```
**Respuesta:**

```json

{
  "id": 1,
  "name": "Leanne Graham",
  "email": "Sincere@april.biz"
}

```
📘 **Ejemplo Post – Crear un nuevo recurso**
```bash
curl -X POST https://jsonplaceholder.typicode.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Ana Torres","email":"ana@mail.com"}'
```

**Respuesta:**
```json
{
  "id": 11,
  "name": "Ana Torres",
  "email": "ana@mail.com"
}
```
---

#### 7.4.2 Postman

**Postman** es una aplicación que permite probar y documentar APIs con una interfaz visual, sin necesidad de escribir comandos.
Es ampliamente usada por desarrolladores y testers para validar endpoints y flujos completos.


📌**Cómo funciona:**

1. Selecciona el método HTTP (GET, POST, PUT, PATCH, DELETE).

2. Escribir la URL del endpoint.

3. Agregar headers y body (por ejemplo, JSON).

4. Ejecutar la solicitud y visualizar la respuesta del servidor formateada.

<div align="center">
<br><em>Interfaz de usuario en Postman</em>
<img src="./images/api\Postman\Postman-v8-user-interface-desktop.gif" alt="🔒 Candado HTTPS" width="600">

</div>

>

📘 **Ejemplo POST en Postman:**

**Método:** POST

**URL:** https://jsonplaceholder.typicode.com/users

**Headers:** Content-Type: application/json

**Body (raw JSON):**

```json
{"name":"Ana Torres","email":"ana@mail.com"}
```

Al presionar Send, Postman muestra el código de estado (`201 Created`) y el cuerpo de la respuesta con el nuevo usuario.

✅ **Ventaja:** Ideal para explorar APIs, probar autenticaciones, generar colecciones de pruebas y documentarlas.

---

#### 7.4.3 Librería Requests en Python

**Requests** es una librería de Python que permite consumir APIs REST desde tu propio programa o script.
Permite automatizar tareas, integrar servicios o construir aplicaciones que interactúan con APIs.

📌**Cómo funciona:**

**1.** Se importa el módulo requests.

**2.** Se ejecuta una función como get(), post(), put(), etc.

**3.** Se recibe una respuesta (response) con atributos como status_code, headers y json().

📘 **Ejemplo POST – Crear un usuario**
```python 
import requests

data = {"name": "Ana Torres", "email": "ana@mail.com"}
response = requests.post("https://jsonplaceholder.typicode.com/users", json=data)

print(response.status_code)  # 201
print(response.json())       # {"id": 11, "name": "Ana Torres", "email": "ana@mail.com"}
```
**Ventaja:**
Ideal para integrar APIs en aplicaciones reales, automatizar procesos o manejar datos dinámicamente desde código Python.

---

### 7.5 Comparativa de herramientas

| **Herramienta**         | **Tipo**            | **Ideal para**                                     | **Ejecución**         |
|--------------------------|--------------------|----------------------------------------------------|------------------------|
| **cURL**                 | Consola            | Pruebas rápidas y depuración técnica de APIs       | Línea de comandos      |
| **Postman**              | Interfaz visual    | Testeo, documentación y automatización de flujos   | Entorno gráfico        |
| **Requests (Python)**    | Código             | Integrar y consumir APIs desde scripts o programas | Código en Python       |


---

## 8. Cabeceras HTTP (Headers)


### 8.1 ¿Qué son las cabeceras?

Las **cabeceras HTTP (headers)** son pares clave-valor que viajan junto con una **solicitud (request)** o una **respuesta (response)**.  
Contienen **metadatos** que describen la naturaleza de la transacción, la identidad del cliente, los formatos de datos aceptados, políticas de seguridad y más.

En otras palabras, las cabeceras son el **lenguaje de control** entre el cliente y el servidor: definen cómo deben procesarse los datos antes, durante y después de la comunicación.

---

🧱 **En la imagen:**
🔹 **Lado izquierdo** → **Solicitud (Request)**

**Headers que aparecen**:


- **Host** → Indica el dominio al que se envía la petición.  
- **User-Agent** → Identifica el cliente (por ejemplo, *curl*).  
- **Accept** → Le dice al servidor qué tipos de respuesta acepta el cliente.  
- **Content-Type** → Informa el formato de los datos enviados (aquí *JSON*).  
- **Content-Length** → Indica cuántos bytes tiene el cuerpo.  

👉 **Importancia:** estas cabeceras garantizan que el servidor reciba correctamente el contenido y pueda responder de forma coherente (por ejemplo, sabiendo si debe interpretar texto, JSON o binarios).
<div align="center">
<br><em></em>
<img src="./images/Header\http-message-anatomy.png" width="600">

</div>

🔹 **Lado derecho** → **Respuesta (Response)**

**Headers que aparecen**:

- **Server** → Indica qué software sirve la respuesta (*Apache*).  
- **Date** → Fecha y hora de la respuesta.  
- **Content-Length** → Tamaño del cuerpo HTML devuelto.  
- **Content-Type** → Tipo de contenido devuelto (*text/html*).  
- **Cache-Control** → Indica que el navegador no debe guardar la página.  

👉 **Importancia:** permiten al cliente interpretar correctamente la respuesta (por ejemplo, saber que el contenido es una página HTML y no un archivo JSON). De esta forma, los **headers HTTP** son como las etiquetas de envío de un paquete:  
no son el contenido principal, pero contienen la información esencial para que el envío y la recepción funcionen correctamente.


---



### 8.2 Tipos y ejemplos de headers comunes

| Tipo | Descripción | Ejemplo |
|------|--------------|----------|
| **Cabeceras generales** | Se aplican tanto a solicitudes como respuestas. | `Date`, `Connection` |
| **Cabeceras de solicitud** | Acompañan las peticiones del cliente e incluyen datos del entorno, autenticación o preferencias. | `User-Agent`, `Authorization`, `Accept` |
| **Cabeceras de respuesta** | Son enviadas por el servidor e indican información sobre la respuesta o el sistema. | `Server`, `Set-Cookie`, `Location` |
| **Cabeceras de entidad** | Describen el contenido del cuerpo de la solicitud o respuesta. | `Content-Type`, `Content-Length`, `Content-Encoding` |

---

### 8.3 Cabeceras comunes en API REST

| Cabecera | Propósito | Ejemplo de uso |
|-----------|------------|----------------|
| **Content-Type** | Indica el formato del cuerpo del mensaje. | `Content-Type: application/json` |
| **Authorization** | Envía credenciales o tokens de autenticación. | `Authorization: Bearer <token>` |
| **Accept** | Especifica el tipo de respuesta que el cliente espera. | `Accept: application/json` |
| **User-Agent** | Identifica el software que realiza la petición. | `User-Agent: Mozilla/5.0` |
| **Cache-Control** | Define reglas sobre almacenamiento en caché. | `Cache-Control: no-cache` |
| **Origin** | Indica el dominio de origen de la solicitud (usado en CORS). | `Origin: https://miapp.cl` |

---

### 🧠 Importancia en el consumo de APIs

Las cabeceras son **cruciales** para:

- Controlar el **tipo de contenido** que se envía o recibe.
- Asegurar **autenticación y seguridad** mediante tokens o claves.
- Gestionar **caché, sesiones y control de flujo**.
- Facilitar la interoperabilidad entre diferentes sistemas y plataformas.

En APIs RESTful, una solicitud sin cabeceras adecuadas puede ser **rechazada o interpretada incorrectamente** por el servidor.



---

## 10. Reflexión personal

























---
## 11. Fuentes

Mozilla Developer Network. (s.f.). HTTP Overview. MDN Web Docs. Recuperado el 30 de octubre de 2025, de https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview

Mozilla Developer Network. (s.f.). HTTPS. MDN Web Docs. Recuperado el 30 de octubre de 2025, de https://developer.mozilla.org/en-US/docs/Glossary/HTTPS

HTTP and HTTPS. (s/f). Stanford.edu. Recuperado el 2 de noviembre de 2025, de https://web.stanford.edu/~ouster/cgi-bin/cs142-spring13/lecture.php?topic=http

Lahey, C., & Go, S. (2021, octubre 20). HTTP vs. HTTPS: Explaining the difference & how to switch. Semrush Blog; Semrush. https://www.semrush.com/blog/http-vs-https/

Difference between http:// and https://. (2015, septiembre 27). GeeksforGeeks. https://www.geeksforgeeks.org/computer-networks/difference-between-http-and-https/


Mozilla Developer Network. (s.f.). Transport Layer Security (TLS) Handshake. MDN Web Docs. Recuperado el 30 de octubre de 2025, de https://developer.mozilla.org/en-US/docs/Web/Security/Transport_Layer_Security

Cloudflare. (s.f.). What happens in a TLS handshake? Cloudflare Learning Center. Recuperado el 30 de octubre de 2025, de https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/

(S/f). Amazon.com. Recuperado el 2 de noviembre de 2025, de https://aws.amazon.com/es/what-is/ssl-certificate/

(S/f-b). Cloudflare.com. Recuperado el 2 de noviembre de 2025, de https://www.cloudflare.com/es-es/learning/ssl/how-does-ssl-work/

W3Schools. (s.f.). HTTP Methods. Recuperado el 30 de octubre de 2025, de https://www.w3schools.com/tags/ref_httpmethods.asp

TCP-IP. (s/f). Microsoft.com. Recuperado el 2 de noviembre de 2025, de https://learn.microsoft.com/es-es/xandr/industry-reference/tcp-ip

(S/f-c). Akamai.com. Recuperado el 2 de noviembre de 2025, de https://www.akamai.com/es/glossary/what-are-ports#:~:text=Web%20(HTTP)%20es%20el%20puerto,DNS%20es%20el%20puerto%2043.

Mozilla Developer Network. (s.f.). HTTP Response Status Codes. MDN Web Docs. Recuperado el 30 de octubre de 2025, de https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

CICS Transaction Server for z/OS. (2025, enero 7). Ibm.com. https://www.ibm.com/docs/es/cics-ts/5.5.0?topic=concepts-status-codes-reason-phrases

Silva, C. (2021, noviembre 1). Códigos HTTP: Lista Completa + Explicaciones. Semrush Blog; Semrush. https://es.semrush.com/blog/codigos-de-estado-http/

Mozilla Developer Network. (s.f.). HTTP Headers. MDN Web Docs. Recuperado el 30 de octubre de 2025, de https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

WebSphere application server network deployment. (2025, junio 30). Ibm.com. https://www.ibm.com/docs/es/was-nd/9.0.5?topic=applications-defining-http-headers-response-codes-restful

(S/f-d). Amazon.com. Recuperado el 2 de noviembre de 2025, de https://aws.amazon.com/es/what-is/restful-api/

¿Qué es una API REST (API RESTful)? (2025, mayo 28). Ibm.com. https://www.ibm.com/es-es/think/topics/rest-apis

IBM Concert. (2025, agosto 19). Ibm.com. https://www.ibm.com/docs/es/concert/2.0.0?topic=common-curl

Uso de cURL. (s/f). Oracle.com. Recuperado el 2 de noviembre de 2025, de https://docs.oracle.com/es-ww/iaas/Content/Identity/api-getstarted/UsecURL.htm

What is postman? (s/f). Postman.com. Recuperado el 2 de noviembre de 2025, de https://www.postman.com/product/what-is-postman/

Python, R. (2025, julio 23). Python’s requests library (guide). Realpython.com; Real Python. https://realpython.com/python-requests/

---


