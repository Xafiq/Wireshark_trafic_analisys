# Wireshark análisis de tráfico
<!-- hide -->

> By [@xafiq](https://github.com/xafiq) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*Esas instrucciones están [available in english](https://github.com/breatheco-de/set-up-an-SSL-in-openSSL-with-a-secure-server/blob/main/README.md)*


# 🌱 Como iniciar este proyecto?

## Requisitos

- Máquina Kali Linux (atacante)
- Debia (victima)
- Máquina Metasploitable (servidor)

## Análisis de tráfico en Wireshark práctico

# 📝 Instrucciones

## 1 - Capturar y analizar el trafico HTTP

### Instrucciones paso a paso:

**Paso 1: Configura Wireshark**

- Abre Wireshark en Kali Linux.
- Haz clic en "Captura" en la barra superior para iniciar la captura de paquetes.

**Paso 2: Aplicar filtro TCP para tráfico HTTP**

- En el cuadro de filtro en la parte inferior de la ventana de Wireshark, escribe `tcp.port == 80` y presiona Enter. Esto capturará todos los tráfico HTTP.

**Paso 3: Realizar una solicitud HTTP en el navegador**

- Abre un navegador web en Debian Linux.
- Navega a la página de inicio de sesión DVWA (por ejemplo, http://[IP-DE-METASPLOITABLE]/dvwa/login.php).
- Ingresa credenciales válidas y envía el formulario.

**Paso 4: Analizar los paquetes capturados**

- En Wireshark, busca el paquete HTTP que coincide con tu intento de inicio de sesión.
- Presta atención a la negociación del handshake TCP (SYN, SYN/ACK, ACK) en los detalles del paquete.

### Explicación del resultado esperado:

- La negociación TCP se verá como tres paquetes consecutivos con banderas y números de secuencia específicos. En la sección de solicitud HTTP, deberías ver el nombre de usuario utilizado para autenticación (por ejemplo, "admin") junto con su contraseña correspondiente.


## 2 - Capturar y analizar ataque XSS

### Instrucciones paso a paso:

**Paso 1: Configura Wireshark**

- Abre Wireshark en Kali Linux.
- Haz clic en "Captura" en la barra superior para iniciar la captura de paquetes.

**Paso 2: Aplicar filtro HTTP desde Kali Linux**

- En el cuadro de filtro en la parte inferior de la ventana de Wireshark, escribe `host [IP-DE-KALI] and http` y presiona Enter. Esto capturará todas las solicitudes HTTP de tu máquina Kali.

**Paso 3: Realizar un ataque XSS en DVWA**

- Abre un navegador web en Kali Linux.
- Navega a la página del sitio DVWA (por ejemplo, http://[IP-DE-METASPLOITABLE]/dvwa/vulnerabilities/xss_r.php).
- Ingresa una carga útil de XSS simple, como `<script>alert('XSS')</script>`, y envía el formulario.

**Paso 4: Analizar los paquetes capturados**

- En Wireshark, busca el paquete HTTP que coincide con tu ataque XSS.
- Deberías ver la línea exacta donde se enviaron las cargas útiles de XSS.


### Explicación del resultado esperado:

- La solicitud HTTP contendrá la carga útil de XSS en su sección de datos. Esta carga puede ser utilizada para ejecutar código JavaScript en el navegador del usuario objetivo.


## 3 - Capturar y analizar la validación del certificado de Google

### Instrucciones paso a paso:

**Paso 1: Configura Wireshark**

- Abre Wireshark en Kali Linux.
- Haz clic en "Captura" en la barra superior para iniciar la captura de paquetes.

**Paso 2: Aplicar filtro HTTP desde Kali Linux**

- En el cuadro de filtro en la parte inferior de la ventana de Wireshark, escribe `host [IP-DE-KALI] and http` y presiona Enter. Esto capturará todas las solicitudes HTTP de tu máquina Kali.

**Paso 3: Realizar una búsqueda en Google**

- Abre un navegador web en Kali Linux.
- Navega a google.com y realiza una búsqueda simple (por ejemplo, "tutorial de Wireshark").

**Paso 4: Analizar los paquetes capturados**

- En Wireshark, busca el paquete HTTP que coincida con tu búsqueda en Google.
- Busca la línea donde se muestra el estado del certificado. Debería indicar si el certificado utilizado en google.com es válido o no.


### Explicación del resultado esperado:

- El resultado de la validación del certificado se mostrará en la sección de negociación SSL/TLS. Si el certificado es válido, verás "OK" al final.



## 4 - Capturar y analizar solicitud a cocacola

### Instrucciones paso a paso:

**Paso 1: Configura Wireshark**

- Abre Wireshark en Kali Linux.
- Haz clic en "Captura" en la barra superior para iniciar la captura de paquetes.

**Paso 2: Aplicar filtro HTTP desde Kali Linux**

- En el cuadro de filtro en la parte inferior de la ventana de Wireshark, escribe `host [IP-DE-KALI] and http` y presiona Enter. Esto capturará todas las solicitudes HTTP de tu máquina Kali.

**Paso 3: Realizar una solicitud al sitio Cocacola**

- Abre un navegador web en Kali Linux.
- Navega a cocacola.com (o cualquier otro sitio de elección).

**Paso 4: Analizar los paquetes capturados**

- En Wireshark, busca el paquete HTTP que coincida con tu solicitud al sitio Cocacola.
- Deberías ver la línea exacta donde se muestra la URL solicitada.


### Explicación del resultado esperado:

- La solicitud HTTP contendrá la URL completa de la página que accediaste (por ejemplo, "GET / HTTP/1.1").


## 5 - Capturar y analizar el archivo my.cnf a través de FTP al servidor Metasploitable desde la máquina Kali Linux

**Paso 1: Configura Wireshark**

- Abre Wireshark en Kali Linux.
- Haz clic en "Captura" en la barra superior para iniciar la captura de paquetes.

**Paso 2: Aplicar filtro FTP**

- En el cuadro de filtro en la parte inferior de la ventana de Wireshark, escribe `port == 21` y presiona Enter. Esto capturará todas las comunicaciones a través del protocolo FTP.

**Paso 3: Conectar via FTP al servidor Metasploitable desde Kali Linux**

- Abre un navegador web en Kali Linux.
- Navega a la carpeta del sitio web (por ejemplo, `ftp://[IP-DE-METASPLOITABLE]`). Asegúrate de que tienes permisos para acceder y descargar archivos.

**Paso 4: Descargar el archivo my.cnf**

- Busca el archivo `my.cnf` en la carpeta del sitio web.
- Haz clic derecho sobre él, selecciona "Descargar" o "Guardar como". Esto descargará el archivo al sistema Kali Linux.

**Paso 5: Analizar los paquetes capturados**

- En Wireshark, busca los paquetes que coincidan con las comunicaciones FTP realizadas durante este proceso.
- Puedes prestar especial atención a la información mostrada por ftp (versión del servidor FTP, usuario utilizado, etc.).


### Explicación del resultado esperado:

- Los paquetes de datos contendrán detalles sobre el archivo `my.cnf` descargado y cualquier otro contenido relacionado con las comunicaciones FTP realizadas.

**Nota:** Asegúrate de que tu configuración de Wireshark esté correctamente filtrada para capturar solo los paquetes relevantes.
