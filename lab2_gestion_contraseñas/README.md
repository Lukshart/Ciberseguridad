# Laboratorio: Ataque y Defensa de Credenciales (MFA)

**Autor:** Matias Alamos Hinojosa  
**Entorno:** Parrot OS (Atacante) / Ubuntu Server (Víctima)

---

## Objetivo del Laboratorio

Demostrar cómo un atacante puede vulnerar una contraseña débil mediante un ataque de diccionario (Hydra) y cómo la implementación de **Autenticación Multifactor (MFA)** con Google Authenticator bloquea el acceso, incluso si la contraseña es comprometida.

## Escenario Simulado

| Elemento | Descripción |
|---|---|
| **Servidor objetivo** | Ubuntu Server con SSH expuesto |
| **Vulnerabilidad inicial** | Contraseña débil (`ubuntu`, `123456`, etc.) |
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

### 2.  Realizar ataque Hydra contra SSH
```bash
hydra -l ubuntu -P rockyou.txt ssh://IP
```

<img width="1200" height="434" alt="image" src="https://github.com/user-attachments/assets/53326c23-f716-4998-ab85-55aa48f8dddb" />

Hydra fue capaz de vulnerar la contraseña mediante un ataque de diccionario.

### 3. Verificar Acceso
```bash
ssh ubuntu@IP
```

<img width="794" height="845" alt="image" src="https://github.com/user-attachments/assets/83644bbe-41f6-47ba-9f66-013d2cad1344" />

### Resultado
Se logró acceder al sistema.

### Fase 2: Hardening - Implementación de MFA

