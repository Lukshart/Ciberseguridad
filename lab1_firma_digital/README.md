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
