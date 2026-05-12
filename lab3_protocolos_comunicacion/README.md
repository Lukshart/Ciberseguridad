# Laboratorio: Protocolos de Comunicación Seguros (HTTPS + SSH Tunneling)

**Autor:** Matias Alamos Hinojosa  
**Entorno:** Kali Linux (Atacante) / Ubuntu Server 22.04.5 (Servidor Web con HTTP)

---

## Objetivo del Laboratorio

Demostrar cómo un atacante puede capturar credenciales en texto plano en tráfico **HTTP** y cómo la implementación de **HTTPS** o **túneles SSH** protege la información haciendo el tráfico ilegible.

---

## Escenario Simulado

| Elemento | Descripción |
|----------|-------------|
| **Servidor web** | Ubuntu con Apache en HTTP (formulario de login) |
| **Vulnerabilidad** | Credenciales viajan en texto plano |
| **Ataque** | Sniffing con Wireshark captura usuario/contraseña |
| **Defensa** | HTTPS (Certbot) + SSH Tunneling |

---

## Comandos y Herramientas Utilizadas

| Herramienta/Comando | Función |
|---------------------|---------|
| `sudo wireshark` | Captura y analiza tráfico de red |
| `http.request.method == "POST"` | Filtro para ver solicitudes POST |
| `sudo certbot --apache` | Configura certificado SSL (Let's Encrypt) |
| `ssh -L 8080:localhost:80 usuario@servidor` | Túnel SSH local |

---

## Procedimiento Paso a Paso

### Fase 1: Sniffing de HTTP (Credenciales en texto plano)

*Nota: Se asume la existencia de un servidor web con un formulario de login funcionando en HTTP.*

#### 1. Iniciar Wireshark
```bash
sudo wireshark
```
Para iniciar la captura de tráfico se debe seleccionar la interfaz de red: Ejemplo `ens33`

<img width="787" height="295" alt="image" src="https://github.com/user-attachments/assets/0f87928b-3ba7-4dd6-9524-3c5a9d3da0cf" />

### 2. Aplicar Filtro
En la barra de filtro, escribir:
```bash
http.request.method == "POST"
```

Muestra solo los paquetes donde el método HTTP es POST

### 3. Acceder al servidor HTTP

<img width="556" height="207" alt="image" src="https://github.com/user-attachments/assets/ab30705d-d7ac-4111-b6a4-f06790343d60" />

---

### 4. Capturar con Wireshark

<img width="1276" height="175" alt="image" src="https://github.com/user-attachments/assets/5739d053-86d7-48ab-bc33-ca13d3b01cff" />

---

Existen dos formas de ver el contenido del paquete se debe hacer lo siguiente:
- Click derecho -> Seguir -> TCP Stream
- `Ctrl + Shift + Alt + T`

<img width="776" height="491" alt="image" src="https://github.com/user-attachments/assets/ca5693f7-8e33-45e5-80bd-288b9165c47e" />

### Resultado
En el método **HTTP** las credenciales viajan sin cifrado (texto plano), por lo que, cualquier atacante que se encuentre en la misma red puede interceptarlas.

---

### Fase 2: Hardening -  Configurar HTTPS con certificado autofirmado
### 1. Certificado autofirmado (local)
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt \
    -subj "/CN=IP_SERVIDOR"
```
Habilitar Módulo SSL
```bash
sudo a2enmod ssl
```
Activar SSL
```bash
sudo a2ensite default-ssl.conf

# Reiniciar Apache
sudo systemctl restart apache2
```

### 2. Sniffing HTTPS

<img width="447" height="203" alt="image" src="https://github.com/user-attachments/assets/24b8aea2-1dfb-4ce1-a00b-9321630b95a4" />

---
**Filtro:**
```bash
tls and ip.dst == 192.168.1.55
```
<img width="1064" height="220" alt="image" src="https://github.com/user-attachments/assets/b621d730-cef8-4204-86e3-d7c92788e523" />

---

<img width="956" height="655" alt="image" src="https://github.com/user-attachments/assets/1965a0e2-5f54-4d4c-ba9c-e4025ae2a50a" />

---

### Resultado
En el método **HTTPS** las credenciales viajan cifradas, por lo que, cualquier atacante que se encuentre en la misma red interceptará tráfico ilegible.

---
### Fase 2: Hardening -  SSH Tunneling
### 1. Crear túnel SSH desde Kali
```bash
ssh -L 8080:localhost:80 ubuntu@[IP_UBUNTU]
```

*Nota: Una vez creado el túnel, se debe mantener la terminal abierta mientras ingrese las credenciales.*

### 2. Acceder a través del túnel

<img width="459" height="201" alt="image" src="https://github.com/user-attachments/assets/461f6f8c-8dae-4e59-8fe3-cc867dc66611" />

### 3. Sniffing con Wireshark
Filtro: `http.request.method == "POST"`

<img width="941" height="249" alt="image" src="https://github.com/user-attachments/assets/dca835dc-3437-4750-9976-a14e8bb12e2d" />

---
Filtro: `ssh`

<img width="1034" height="273" alt="image" src="https://github.com/user-attachments/assets/0da03ff4-3683-4848-b1b8-c4f2b5eeac29" />

---

<img width="954" height="436" alt="image" src="https://github.com/user-attachments/assets/6a30c15b-b0b6-460d-af8e-43f51c66728e" />

---
### Resultados y Comparaciones
Mediante Tunneling incluso **HTTP** resulta ilegible.

| Método | ¿Credenciales visibles? | Seguridad |
|---|---|---|
| HTTP | Sí | Nula |
| HTTPS | No | Alta |
| SSH Tunneling | No | Alta

---
### Conclusiones Finales
- El laboratorio demuestra que el tráfico HTTP viaja en texto plano y puede ser interceptado fácilmente.
- La implementación de HTTPS o el uso de túneles SSH cifran las comunicaciones, haciendo que las credenciales sean ilegibles para un atacante.

**Aplicación Defensiva:**
| Acción | Implementación |
|---|---|
| Prevención | Todo sitio que maneje credenciales debe usar HTTPS
| Detección | Wireshark permite verificar si hay tráfico HTTP no cifrado |
| Respuesta | Migrar servicios inseguros a HTTPS o túneles SSH |

**Cumplimiento Ley 21.663:**
| Requisito | Implementación |
|---|---|
| Protección de datos | HTTPS cifra comunicaciones |
| Confidencialidad | TLS evita exposición en texto plano |
| Seguridad | SSH tunneling como capa adicional | 

---
### Recomendaciones
| Prioridad | Medida | Fundamento |
|---|---|---|
| 🔴 Alta | Todo sitio debe usar HTTPS | Credenciales nunca en texto plano |
| 🔴 Alta | Configurar redirección HTTP → HTTPS | Evita que usuarios accedan por error a HTTP |
| 🟡 Media | Usar SSH tunneling para servicios internos | Protege tráfico sin certificado |
| 🟡 Media | Monitorear tráfico sospechoso | Detectar servicios inseguros en la red |
