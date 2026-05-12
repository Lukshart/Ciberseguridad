# Laboratorio: Ataque y Defensa de Credenciales (MFA)

**Autor:** Matias Alamos Hinojosa  
**Entorno:** Parrot OS (Atacante) / Ubuntu Server 22.04.5 (Víctima)

---

## Objetivo del Laboratorio

Demostrar cómo un atacante puede vulnerar una contraseña débil mediante un ataque de diccionario (Hydra) y cómo la implementación de **Autenticación Multifactor (MFA)** con Google Authenticator bloquea el acceso, incluso si la contraseña es comprometida.

## Escenario Simulado

| Elemento | Descripción |
|---|---|
| **Servidor objetivo** | Ubuntu Server con SSH expuesto |
| **Vulnerabilidad inicial** | Contraseña débil (`ubuntu`, `admin123`, etc.) |
| **Ataque** | Hydra realiza fuerza bruta contra SSH |
| **Defensa implementada** | MFA con Google Authenticator (contraseña + token temporal) |

---

## Comandos y Herramientas Utilizadas

| Herramienta/Comando | Función |
|---|---|
| `hydra -l usuario -P diccionario.txt ssh://IP` | Ataque de diccionario contra SSH |
| `ssh usuario@IP` | Intento de conexión legítima |
| `sudo apt install libpam-google-authenticator` | Instala módulo PAM para MFA |
| `google-authenticator` | Configura MFA para el usuario |
| `nano /etc/pam.d/sshd` | Configura PAM para requerir MFA |
| `nano /etc/ssh/sshd_config` | Configura SSH para usar MFA |
| `sudo systemctl restart sshd` | Aplica cambios |

---

## Procedimiento Paso a Paso

### Fase 1: Ataque Inicial (Sin MFA)

#### 1. Preparar el diccionario (Kali Linux)
Para este laboratorio se hará uso del diccionario common-passwords-win.txt, proveniente de: [SectList](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/common-passwords-win.txt)

### 2. Realizar ataque Hydra contra SSH
```bash
hydra -l ubuntu -P rockyou.txt ssh://IP
```

<img width="1200" height="434" alt="image" src="https://github.com/user-attachments/assets/53326c23-f716-4998-ab85-55aa48f8dddb" />

### 3. Verificar Acceso
```bash
ssh ubuntu@IP
```

<img width="794" height="845" alt="image" src="https://github.com/user-attachments/assets/83644bbe-41f6-47ba-9f66-013d2cad1344" />

### Resultado
Se logró acceder al sistema.

### Fase 2: Hardening - Implementación de MFA
### 1.Instalar Google Authenticator PAM
```bash
sudo apt install libpam-google-authenticator -y
```

### 2. Configurar MFA para el usuario
```bash
google-authenticator
```
Configuración deseada.

| Configuración | Argumento | Efecto |
|---|---|---|
| Do you want authentication tokens to be time-based? | `y` | Tokens temporales |
| Do you want me to update your "~/.google_authenticator" file? | `y` | Guarda configuración |
| Do you want to disallow multiple uses of the same token? | `y` | Evita reuso de tokens |
| Do you want to increase the original window size? | `n` | Mantiene ventana de tiempo entre tokens |
| Do you want to enable rate-limiting? | `y` | Limita intentos fallidos |

### 3. Configurar SSH para usar MFA
Para activar la autenticación multifactor es necesario modificar los siguientes archivos:
- `/etc/pam.d/sshd`
- `/etc/ssh/sshd_config`
```bash
sudo nano /etc/pam.d/sshd
```

Se añade `auth google pam_google_authenticator.so`

<img width="816" height="615" alt="image" src="https://github.com/user-attachments/assets/ef445ef4-6dcb-4bcb-9615-bf03d7d18b98" />

---

```bash
sudo nano /etc/ssh/sshd_config
```

Se modifican y se añaden las siguientes líneas:
```bash

KbdInteractiveAuthentication yes
UsePAM yes

```

<img width="817" height="231" alt="image" src="https://github.com/user-attachments/assets/7c4577df-7dba-40ab-886b-45609bd7c0e0" />

### 4. Prueba de Defensa
El atacante nuevamente intenta ingresar al servidor a través de SSH.
```bash
ssh ubuntu@IP
```

<img width="652" height="169" alt="image" src="https://github.com/user-attachments/assets/5201e65f-d041-4ad2-8d07-64493fc8ca14" />

---

Tras 3 intentos fallidos, el sistema bloquea al host.

<img width="481" height="318" alt="image" src="https://github.com/user-attachments/assets/8522a5cc-95fc-4730-8857-ddd0f82f556c" />

---

Logs desde el servidor.

<img width="837" height="367" alt="image" src="https://github.com/user-attachments/assets/16ab173e-0f10-4f16-a857-33ece990332d" />

---

### Conclusiones Finales
- Las contraseñas por sí solas son insuficientes.
- La implementación de Autenticación Multifactor (MFA) agrega una capa defensiva crítica que bloquea el acceso incluso si la contraseña es comprometida.

**Posibles vectores de ataque**
| Vulnerabilidad | Mitigación | 
|---|---|
| Fuerza bruta/diccionario | No es suficiente sola |
| Phishing, reuso, filtraciones | Ataque requiere TOKEN | 
| Captura de tráfico | Tokens expiran (30 segundos) |

**¿Por qué MFA es importante?**

Las contraseñas se roban, filtran o adivinan. MFA añade una segunda capa (algo que tienes) que el atacante no posee.

---

**Aplicación Defensiva:**
| Acción | Implementación | 
|---|---|
| Prevención | MFA bloquea acceso incluso con contraseñas comprometidas |
| Detección | Logs muestran intentos fallidos | 
| Respuesta | Rate limiting dificulta ataques automatizados |

**Cumplimiento Ley 21.663:**
| Requisito | Implementación | 
|---|---|
| Control de acceso a sistemas críticos | Exige medidas proporcionales al riesgo. |
| Protección contra acceso no autorizado | Segundo factor impide acceso solo con credenciales |
| Trazabilidad | Logs de intentos de acceso |

---

### Recomendaciones en entornos productivos
| Prioridad | Medida | Fundamento |
|---|---|---|
| 🔴 Alta | MFA obligatorio | Todo acceso SSH debe requerir contraseña + token |
| 🔴 Alta | Rate limiting | Prevenir fuerza bruta al MFA | 
| 🟡 Media | Monitoreo | Logs para detectar intentos fallidos |
