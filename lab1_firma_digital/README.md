# Laboratorio: Firma Digital y Verificación de Integridad
**Autor:** Matias Alamos Hinojosa   
**Entorno:** Parrot OS (Auditor)

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

cat > config_bancaria.txt << 'EOF'
CUENTA_ORIGEN=12345678
MONTO=1000000
EOF
```
<img width="479" height="312" alt="image" src="https://github.com/user-attachments/assets/7a51fb53-ed14-41ef-99df-2b041062b6b3" />

### 2. Generar hash del archivo
```bash
sha256sum config_bancaria.txt
```
<img width="882" height="192" alt="image" src="https://github.com/user-attachments/assets/f9efa2db-6a01-461d-95f8-9d004ac24ed4" />

### 3. Simular ataque (modificación de un bit)
```bash
# El atacante cambia un 0 por un 1 en el monto
sed -i 's/1000000/1000001/' config_bancaria.txt
```
<img width="547" height="245" alt="image" src="https://github.com/user-attachments/assets/3cedcbc1-7e5a-41cc-91b8-cac3248e1789" />

### 4. Verificar hash
```bash
sha256sum config_bancaria.txt
```
<img width="881" height="185" alt="image" src="https://github.com/user-attachments/assets/4a27905a-fae5-4335-a915-398b181271f6" />

### 5. Conclusión
Un cambio microscópico produce un efecto bola de nieve en el hash.

### 6. Generar llaves RSA
Generar llave privada:
```bash
openssl genrsa -out privada.pem 2048
```
| Argumento | Función |
|---------|---------|
| `genrsa` | Generar llave RSA |
| `-out privada.pem` | Guardar la llave en un archivo llamado `privada.pem` |
| `2048` | Tamaño de la llave (en bits) |

`.pem` es una extensión utilizada como estándar para almacenar certificados, llaves criptográficas y firmas digitales.

La llave dispondrá un formato similar

```bash
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC7...
... (texto ilegible pero en letras/números) ...
-----END PRIVATE KEY-----
```

---

Extraer llave pública a partir de la llave privada:
```bash
# Extraer llave pública
openssl rsa -in privada.pem -pubout -out publica.pem
```

| Argumento | Función |
|---------|---------|
| `rsa` | Argumento para manejar llaves RSA |
| `-in privada.pem` | Archivo de entrada (la llave privada) |
| `-pubout` | Extraer la llave PÚBLICA |
| `-out publica.pem` | Guardar la llave pública en este archivo |

<img width="656" height="299" alt="image" src="https://github.com/user-attachments/assets/591c8a0d-4f45-4419-b1e6-cd75656e62b9" />

### 7. Firmar el archivo 
```bash
openssl dgst -sha256 -sign privada.pem -out firma.bin config_bancaria.txt
```

| Argumento | Función |
|---------|---------|
| `dgst` | Digest (resumen / hash) - calcula y procesa hashes |
| `-sha256` | Algoritmo hash SHA-256 |
| `-sign privada.pem` | Firma usando la llave privada |
| `-out firma.bin` | Guarda el resultado (la firma) en el archivo firma.bin |
| `config_bancaria.txt` | El archivo a firmar |

### 8. Verificar el archivo 
```bash
openssl dgst -sha256 -verify publica.pem -signature firma.bin config_bancaria.txt
```

| Argumento | Función |
|---------|---------|
| `dgst` | Digest (resumen / hash) - calcula y procesa hashes |
| `-sha256` | Algoritmo hash SHA-256 |
| `-verify publica.pem` | Verifica la firma usando la llave pública |
| `-signature firma.bin` | El archivo de firma que se generó previamente |
| `config_bancaria.txt` | El archivo a verificar |

<img width="885" height="174" alt="image" src="https://github.com/user-attachments/assets/e8044933-4f9d-4869-8775-81d9cf8e9204" />

### 8. Demostrar que una modificación invalida la firma
Modificamos el archivo:
```bash
sed -i 's/1000001/9999999/' config_bancaria.txt
```
<img width="541" height="190" alt="image" src="https://github.com/user-attachments/assets/770e2a1b-e0b5-498a-ba7b-581cacc251b1" />


Verificamos el archivo:
```bash
openssl dgst -sha256 -verify publica.pem -signature firma.bin config_bancaria.txt
```
<img width="1336" height="171" alt="image" src="https://github.com/user-attachments/assets/814b504c-8123-4f10-8fc9-d18bf35bd3ad" />
