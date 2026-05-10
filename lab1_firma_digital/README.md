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

### Conclusión sobre el hash
Un cambio microscópico produce un efecto bola de nieve en el hash.

### 5. Generar llaves RSA
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

### 6. Firmar el archivo 
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

### 7. Verificar el archivo 
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

---
Verificamos el archivo:
```bash
openssl dgst -sha256 -verify publica.pem -signature firma.bin config_bancaria.txt
```
<img width="1336" height="171" alt="image" src="https://github.com/user-attachments/assets/814b504c-8123-4f10-8fc9-d18bf35bd3ad" />

---

### Caso de ejemplo

**Contexto:** Un banco chileno desarrolla una actualización crítica para su aplicación de transferencias. El software pasa por el pipeline de integración continua y debe ser desplegado en servidores de producción.

**Riesgo:** Un atacante modifica el binario o sus configuraciones durante la transferencia del artefacto entre el pipeline de integración continua y el servidor de producción.

**Solución:** Firmar digitalmente un manifiesto que contiene los hashes de todos los archivos del despliegue.

### 1. Hashear cada uno de los archivos (Desarrollo)
Estructura del directorio:

<img width="621" height="216" alt="image" src="https://github.com/user-attachments/assets/185e748a-2cbc-4493-a478-0c3a92356ffb" />

---

```bash
find transferencias -type f -exec sha256sum {} \; | sort > MANIFIESTO.txt
```

| Argumento | Función |
|---------|---------|
| `find transferencias -type f` | Busca todos los archivos dentro de la carpeta |
| `-exec sha256sum {} \;` | Calcula el hash SHA-256 de cada archivo |
| `sort` | Ordena alfabéticamente los resultados |
| `> MANIFIESTO.txt` | Guarda la lista en el archivo MANIFIESTO.txt |

<img width="1109" height="173" alt="image" src="https://github.com/user-attachments/assets/fc716fcf-545a-4a92-8a72-99cfedc3f10f" />

### 2. Firmar el manifiesto con la llave privada
```bash
openssl dgst -sha256 -sign privada.pem -out MANIFIESTO.sig MANIFIESTO.txt
```

---

### 3. Verificación de manifiesto (Despliegue)
Antes de un despliegue, el equipo debe verificar que los archivos provienen de una fuente autorizada.
```bash
openssl dgst -sha256 -verify publica.pem -signature MANIFIESTO.sig MANIFIESTO.txt
```
<img width="877" height="71" alt="image" src="https://github.com/user-attachments/assets/44f67904-1976-4d7a-9c30-1de3a9aa4fbe" />

### 4. Verificación de los archivos
Una vez se comprobada la veracidad de la firma se recomienda verificar cada archivo individualmente para evitar fraudes post-firma.
```bash
find transferencias -type f -exec sha256sum {} \; | sort > MANIFIESTO_actual.txt
```

<img width="465" height="247" alt="image" src="https://github.com/user-attachments/assets/fb4605c5-7623-427f-b056-a39a79f0ea81" />

---

Se comparan ambos archivos.

```bash
diff MANIFIESTO.txt MANIFIESTO_actual.txt; echo $?
```
| Código | Significado |
|---------|---------|
| `0` | Archivos iguales |
| `1` | Archivos diferentes |
| `2` | Error |

<img width="583" height="135" alt="image" src="https://github.com/user-attachments/assets/ed22307e-7c56-4cd3-9d10-5c7b0ce9be97" />

### 5. Simular manipulación
Se realizan cambios sutiles
```bash
#ANTES
┌─[luk@parrot]─[~/Desktop/lab1_firma_digital/transferencias]
└──╼ $cat conf
conf

┌─[luk@parrot]─[~/Desktop/lab1_firma_digital/transferencias/credentials]
└──╼ $ cat admin_credentials
USER=admin
PASS=2314
```
```bash
#DESPUÉS
┌─[luk@parrot]─[~/Desktop/lab1_firma_digital/transferencias]
└──╼ $cat conf
conf
alterada

┌─[luk@parrot]─[~/Desktop/lab1_firma_digital/transferencias/credentials]
└──╼ $ cat admin_credentials
USER=admin
PASS=admin
```
### 6. Recalcular el manifiesto actual (después de la manipulación)
```bash
find transferencias -type f -exec sha256sum {} \; | sort > MANIFIESTO_actual.txt
```

### 7. Comparar errores
```bash
diff MANIFIESTO.txt MANIFIESTO_actual.txt

echo $?
```

<img width="1135" height="305" alt="image" src="https://github.com/user-attachments/assets/e1ddc01d-7dd8-462b-b018-bb3484a187f3" />

---

El código `2,3c2,3` indica que las líneas 2 y 3 del archivo original `MANIFIESTO.txt` fueron cambiadas `c` por las líneas 2 y 3 del archivo `MANIFIESTO_actual.txt`, mientras que el código `1` afirma que existe una **MODIFICACIÓN** en los archivos.

---

### Conclusión final
El laboratorio demuestra que la firma digital y la verificación de integridad son controles esenciales para proteger Organizaciones de Importancia Vital (OIV) según la Ley 21.663.

**Aplicación defensiva:**

| Acción | Implementación |
|---------|---------|
| Prevención | Firmar manifiestos antes del despliegue evita la ejecución de software manipulado |
| Detección | La comparación de hashes (`diff` + código `1`) alerta sobre modificaciones no autorizadas |
| Respuesta | El pipeline debe detenerse automáticamente ante cualquier falla de verificación |

**Cumplimiento Ley 21.663:**

| Requisito legal | Cumplimiento |
|---------|---------|
| Integridad de activos críticos | Los hashes detectan cualquier alteración |
| Trazabilidad de acciones | La firma digital provee no repudio |
| Reporte oportuno al CSIRT | La detección automática permite notificar < 3 horas |

### Recomendaciones
| Prioridad | Medida |
|---------|---------|
| Alta | Firmar **TODOS** los binarios y configuraciones antes de producción |
| Alta | Verificar firma Y hashes en cada despliegue |
| Alta | Rotar la llave cada 6 - 12 meses |
| Media | Almacenar llaves privadas en vaults |
| Media | Automatizar bloqueo del pipeline si falla verificación |
