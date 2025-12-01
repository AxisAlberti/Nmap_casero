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





## Introducción breve a Nmap

Nmap (Network Mapper) es una herramienta libre y de código abierto destinada a explorar redes y evaluar su seguridad. [web:83][web:81] Permite descubrir equipos conectados, identificar puertos abiertos, servicios activos y, en muchos casos, el sistema operativo y las versiones de software que se están ejecutando. [web:84][web:85]  

Funciones principales de Nmap:  
- Descubrimiento de hosts y creación de inventarios de red. [web:84][web:94]  
- Escaneo de puertos TCP/UDP y detección de servicios y versiones (opción `-sV`). [web:81][web:88]  
- Detección de sistema operativo mediante análisis de huellas de la pila TCP/IP. [web:81][web:92]  
- Uso del motor de scripts NSE (Nmap Scripting Engine) para comprobar vulnerabilidades y configuraciones inseguras. [web:81][web:89]  

---

## Uso de Nmap por peritos informáticos

Los peritos informáticos y analistas forenses utilizan Nmap como herramienta de apoyo en investigaciones de incidentes de seguridad y en la elaboración de informes periciales. [web:86][web:87] Su finalidad es documentar de forma precisa el estado de una red o equipo en un momento determinado, no atacar sistemas.  

Algunos usos habituales en el ámbito pericial son:  
- **Reconstrucción del estado de la red durante un incidente:** Nmap se emplea para identificar qué equipos están activos, qué puertos permanecen abiertos y qué servicios están expuestos en un intervalo de tiempo concreto, generando una “fotografía” técnica que se incorpora al informe pericial. [web:86][web:90]  
- **Detección de servicios anómalos o no autorizados:** al comparar los resultados del escaneo con la configuración esperada, el perito puede localizar puertos inesperados, servicios ocultos o versiones desactualizadas de software que pueden haber sido utilizadas como vector de ataque. [web:86][web:89]  
- **Delimitación del alcance de una intrusión:** los escaneos ayudan a identificar qué sistemas presentan indicios de compromiso o cambios relevantes en sus servicios, colaborando en la delimitación de daños y en la cadena de evidencias. [web:86][web:87]  
- **Soporte a la redacción del informe técnico:** los resultados exportados por Nmap (en formatos de texto o XML) permiten documentar qué pruebas se realizaron, con qué parámetros y en qué momento, aportando trazabilidad y rigor metodológico al dictamen pericial. [web:86][web:98][web:95]
