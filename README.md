# Nmap_casero
## Práctica: Implementación de un “mini‑Nmap” casero en Python

### Introducción

En esta práctica se desarrollará un pequeño escáner de puertos en Python que imita, de forma muy simplificada, el comportamiento de una herramienta de análisis de red. El objetivo es que el alumnado reutilice código de prácticas anteriores (gestión de argumentos, manejo de errores, uso de funciones) para construir un programa ejecutable desde línea de comandos.

---

### Objetivo de la práctica

Desarrollar un módulo en Python capaz de:

- Aceptar una dirección IP de destino y una lista opcional de puertos desde la línea de comandos.  
- Escanear los puertos indicados o, en su defecto, un conjunto de puertos predefinidos.  
- Mostrar por pantalla qué puertos están accesibles y cuáles no responden.

---

### Especificación funcional

El programa se ejecutará desde terminal con la siguiente sintaxis:

nombre_modulo.py ip [opciones] 

Donde:

- `ip` es la dirección IP del host que se desea analizar.  
- `[opciones]` es un bloque opcional de parámetros.

Para esta primera versión se utilizará la opción:

-p lista_puertos


#### Comportamiento esperado

1. **Sin opción `-p`**  
   - Si el usuario solo indica la IP:

     ```
     nombre_modulo.py 192.168.1.10
     ```

   - El programa deberá escanear un conjunto de puertos por defecto (que se definirá posteriormente: por ejemplo, varios puertos habituales de servicios conocidos).

2. **Con opción `-p lista_puertos`**  
   - Si el usuario indica:

     ```
     nombre_modulo.py 192.168.1.10 -p 22,80,443
     ```

   - El programa solo escaneará los puertos indicados en `lista_puertos`.  
   - La lista de puertos deberá validarse:
     - Solo valores numéricos enteros.  
     - Sin duplicados.  
     - Dentro del rango permitido (1–65535).

En ambos casos, para cada puerto analizado el programa intentará establecer una conexión y determinar si el puerto está “abierto” (acepta conexión) o “cerrado/no accesible”.

---

### Requisitos técnicos

El módulo deberá:

- Leer y validar los argumentos de línea de comandos:
  - Número correcto de parámetros.  
  - Formato de la opción `-p`.  
  - Formato de la lista de puertos, cuando exista.  

- Reutilizar funciones ya trabajadas previamente para:
  - Procesar argumentos.  
  - Convertir cadenas a enteros de forma segura.  
  - Gestionar y mostrar mensajes de error.

- Implementar la lógica de escaneo de puertos:
  - Intentar la conexión al puerto correspondiente.  
  - Establecer un tiempo de espera razonable.  
  - Cerrar correctamente los recursos utilizados.  

- Gestionar de forma controlada:
  - Direcciones IP no válidas o no alcanzables.  
  - Formatos incorrectos en la lista de puertos.  
  - Falta de argumentos obligatorios.

#### Salida por pantalla

Para cada puerto analizado se mostrará una línea similar a:

- `Puerto 80: ABIERTO`  
- `Puerto 22: CERRADO`  

Al finalizar, se puede mostrar un pequeño resumen del número total de puertos analizados y cuántos se han encontrado abiertos.

---

### Entregables

El alumnado deberá entregar:

- El archivo `nombre_modulo.py` con el código del escáner de puertos.  
- Un archivo `README.md` que incluya:
  - Descripción breve del programa.  
  - Sintaxis de uso.  
  - Uno o dos ejemplos de ejecución con y sin opción `-p`.  
  - Posibles mejoras que se podrían incorporar en futuras versiones.

---

## Puertos TCP/UDP más utilizados

| Puerto | Protocolo | Servicio principal                    | Uso habitual resumido                                                    |
|--------|-----------|---------------------------------------|---------------------------------------------------------------------------|
| 20     | TCP       | FTP-data                              | Canal de datos para transferencias FTP clásicas. [web:120][web:125]      |
| 21     | TCP       | FTP                                   | Control de sesiones FTP para transferencia de archivos. [web:120][web:125] |
| 22     | TCP       | SSH                                   | Acceso remoto seguro por consola y tunelización. [web:120][web:125]      |
| 23     | TCP       | Telnet                                | Acceso remoto sin cifrar (obsoleto/inseguro). [web:120][web:125]         |
| 25     | TCP       | SMTP                                  | Envío de correo electrónico entre servidores. [web:120][web:124]         |
| 53     | TCP/UDP   | DNS                                   | Resolución de nombres de dominio a direcciones IP. [web:120][web:125]    |
| 67/68  | UDP       | DHCP                                  | Asignación dinámica de direcciones IP en redes. [web:120][web:124]       |
| 69     | UDP       | TFTP                                  | Transferencia simple de archivos, sin autenticación. [web:120][web:124]  |
| 80     | TCP       | HTTP                                  | Tráfico web no cifrado (páginas web). [web:120][web:125]                 |
| 110    | TCP       | POP3                                  | Recepción y descarga de correo en clientes. [web:120][web:125]           |
| 123    | UDP       | NTP                                   | Sincronización horaria de sistemas en red. [web:120][web:125]            |
| 143    | TCP       | IMAP                                  | Acceso y gestión de correo en el servidor. [web:120][web:125]            |
| 161    | UDP       | SNMP                                  | Monitorización y gestión de dispositivos de red. [web:120][web:125]      |
| 389    | TCP/UDP   | LDAP                                  | Directorios centralizados de usuarios y recursos. [web:120][web:125]     |
| 443    | TCP       | HTTPS                                 | Tráfico web cifrado (HTTP sobre TLS/SSL). [web:120][web:125]             |
| 445    | TCP       | SMB / Microsoft-DS                    | Compartición de archivos e impresoras en Windows. [web:120][web:125]     |
| 465/587| TCP       | SMTPS / Submission                    | Envío autenticado y cifrado de correo saliente. [web:120][web:125]       |
| 993    | TCP       | IMAPS                                 | Acceso cifrado a correo IMAP. [web:120][web:125]                          |
| 995    | TCP       | POP3S                                 | Acceso cifrado a correo POP3. [web:120][web:125]                          |
| 1433   | TCP       | Microsoft SQL Server                  | Servicio de base de datos SQL Server. [web:120][web:135]                 |
| 1521   | TCP       | Oracle SQL*Net                        | Conexiones cliente-servidor a bases Oracle. [web:120][web:135]           |
| 3306   | TCP       | MySQL / MariaDB                       | Servicio de base de datos MySQL/MariaDB. [web:120][web:133]              |
| 3389   | TCP       | RDP                                   | Escritorio remoto de Windows. [web:120][web:125]                          |
| 5432   | TCP       | PostgreSQL                            | Servicio de base de datos PostgreSQL. [web:120][web:133]                 |
| 5900   | TCP       | VNC                                   | Escritorio remoto multiplataforma (VNC). [web:120][web:136]              |
| 8080   | TCP       | HTTP alternativo / proxys             | Servicios web alternativos o proxys HTTP. [web:120][web:136]             |
