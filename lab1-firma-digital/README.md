# Laboratorio: Firma Digital y Verificación de Integridad

**Autor:** Matias Alamos Hinojosa   
**Entorno:** Parrot OS (Auditor) | Ubuntu Server (Producción)

---

## Objetivo del Laboratorio

Demostrar cómo la criptografía asimétrica (firma digital) permite garantizar la **integridad** y **autenticidad** de archivos críticos, simulando un escenario real donde un archivo de configuración bancaria debe ser firmado antes de subirse a producción.

---

## Escenario Simulado

| Elemento | Descripción |
|----------|-------------|
| **Archivo crítico** | `config_bancaria.txt` (montos, cuentas, fechas) |
| **Riesgo** | Un atacante modifica el monto de una transferencia |
| **Solución** | Firma digital con llave privada / verificación con llave pública |

---

## Comandos Utilizados

| Comando | Función |
|---------|---------|
| `sha256sum archivo` | Genera hash SHA-256 |
| `openssl genrsa -out privada.pem 2048` | Genera llave privada RSA |
| `openssl rsa -in privada.pem -pubout -out publica.pem` | Extrae llave pública |
| `openssl dgst -sha256 -sign privada.pem -out firma.bin archivo` | Firma digitalmente un archivo |
| `openssl dgst -sha256 -verify publica.pem -signature firma.bin archivo` | Verifica firma |

---

## Procedimiento Paso a Paso

### 1. Crear el archivo de configuración

```bash
mkdir ~/lab1_firma_digital
cd ~/lab1_firma_digital

cat > config_bancaria.txt

CUENTA_ORIGEN=12345678
MONTO=1000000
