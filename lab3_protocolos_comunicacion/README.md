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
```bash
http.request.method == "POST"
```

Muestra solo los paquetes donde el método HTTP es POST

### 3. Acceder al servidor HTTP

<img width="556" height="207" alt="image" src="https://github.com/user-attachments/assets/ab30705d-d7ac-4111-b6a4-f06790343d60" />

---

### 4. Observar en Wireshark

<img width="1276" height="175" alt="image" src="https://github.com/user-attachments/assets/5739d053-86d7-48ab-bc33-ca13d3b01cff" />

---

Existen dos formas de ver el contenido del paquete se debe hacer lo siguiente:
- Click derecho -> Seguir -> TCP Stream
- `Ctrl + Shift + Alt + T`

<img width="776" height="491" alt="image" src="https://github.com/user-attachments/assets/ca5693f7-8e33-45e5-80bd-288b9165c47e" />

### Resultado
En el método **HTTP** las credenciales viajan sin cifrado (texto plano), por lo que, cualquier atacante que se encuentre en la misma red puede interceptarlas.
