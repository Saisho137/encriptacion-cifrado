# 🛡️ Guía de Seguridad Web: Criptografía Aplicada

Esta es una guía de estudio completa sobre los conceptos de seguridad web, con un enfoque profundo en criptografía (encriptación y hashing), diseñada para preparar Assessments de nivel Mid-Senior para roles Full Stack y para servir como referencia técnica integral.

---

## 📑 Tabla de Contenidos

1. [Conceptos Fundamentales](#1-fundamentos-criptografía-encriptación-o-cifrado)
2. [Historia y Tipos de Ataques Criptográficos](#2-historia-y-tipos-de-ataques-criptográficos)
3. [Cifrado Simétrico](#3-cifrado-simétrico-)
4. [Cifrado Asimétrico](#4-cifrado-asimétrico--)
5. [Funciones Hash](#5-funciones-hash-la-huella-digital-de-los-datos)
6. [Casos de Uso en la Web](#6-casos-de-uso-en-la-web)
7. [Análisis Comparativo de Rendimiento](#7-análisis-comparativo-de-rendimiento)
8. [Cifrado en Reposo vs Cifrado en tránsito](#8-cifrado-en-reposo-vs-cifrado-en-tránsito)
9. [Patrones de Seguridad Web Aplicados](#9-patrones-de-seguridad-web-aplicados)
10. [Buenas Prácticas y Resumen](#10-buenas-prácticas-y-resumen)

---

## 1. Fundamentos: ¿Criptografía, Encriptación o Cifrado?

Para empezar, aclaremos los términos. Aunque a menudo se usan indistintamente, tienen matices específicos:

### Definiciones Precisas

- **Criptografía**: Es la **disciplina** o el campo de estudio de las técnicas de comunicación segura en presencia de terceros (adversarios). Abarca mucho más que solo "esconder" mensajes; incluye técnicas para la autenticación, integridad de datos y no repudio. Es el paraguas que lo cubre todo.

- **Cifrado o Encriptación**: Estos dos términos **son sinónimos**. Se refieren al **proceso** específico de tomar un mensaje legible (llamado *texto plano* o *plaintext*) y convertirlo en un formato ilegible (llamado *texto cifrado* o *ciphertext*) usando un algoritmo y una clave.

- **Descifrado o Desencriptación**: Es el proceso inverso: convertir el texto cifrado de nuevo a texto plano, usando la clave correcta.

> **No hay diferencia práctica** entre "encriptación" y "cifrado" en el contexto de seguridad informática. Ambos términos se usan intercambiablemente.
> **Analogía 🧠:** Piensa en la **Criptografía** como la *ingeniería de cerraduras y cajas fuertes*. La **Encriptación** sería el *acto de girar la llave para cerrar la caja fuerte*.

### Elementos Básicos del Proceso Criptográfico

#### 1. **Texto Plano (Plaintext)**

- Información original legible
- Ejemplo: "Información confidencial"

#### 2. **Texto Cifrado (Ciphertext)**  

- Información transformada e ilegible
- Ejemplo: `496e666f726d6163696f6e20636f6e666964656e6369616c` (hexadecimal)

#### 3. **Algoritmo de Cifrado**

- Función matemática que realiza la transformación
- Ejemplos: AES, RSA, ChaCha20

#### 4. **Clave (Key)**

- Parámetro secreto usado por el algoritmo
- Su longitud determina la fortaleza del cifrado

#### 5. **Descifrado (Decryption)**

- Proceso inverso que convierte texto cifrado a texto plano

### Principios de Seguridad (CIA Triad)

#### **Confidencialidad (Confidentiality)**

- Solo personas autorizadas pueden acceder a la información
- Implementado principalmente a través del cifrado

#### **Integridad (Integrity)**

- La información no ha sido alterada
- Implementado con funciones hash y firmas digitales

#### **Disponibilidad (Availability)**

- La información está accesible cuando se necesita
- Implementado con redundancia y sistemas distribuidos

---

## 2. Historia y Tipos de Ataques Criptográficos

### Evolución de la Criptografía

#### **Cifrados Clásicos**

- **César**: Desplazamiento de letras (ROT13)
- **Vigenère**: Clave repetitiva
- **Enigma**: Máquina de cifrado mecánica

#### **Era Moderna**

- **DES (1977)**: Primer estándar de cifrado
- **AES (2001)**: Estándar actual
- **Criptografía cuántica**: Futuro de la seguridad

#### **El Problema Cuántico**

Las computadoras cuánticas representan una amenaza existencial para la criptografía actual:

- **Algoritmo de Shor**: Puede factorizar números grandes eficientemente, rompiendo RSA y ECC
- **Algoritmo de Grover**: Reduce la seguridad de algoritmos simétricos a la mitad

**Cronología estimada**:

- **2030-2035**: Computadoras cuánticas podrían romper RSA-2048
- **2040-2050**: RSA-4096 y curvas elípticas en riesgo

### Tipos de Ataques Criptográficos

#### **1. Ataques de Fuerza Bruta**

- **Concepto**: Probar todas las combinaciones posibles de claves
- **Complejidad**: O(2^n) donde n es la longitud de la clave en bits
- **Mitigación**: Claves largas (256+ bits), algoritmos lentos para contraseñas

#### **2. Ataques de Diccionario**

- **Concepto**: Usar claves comunes, predecibles o derivadas de palabras
- **Mitigación**: Claves aleatorias, salt en contraseñas, entropía alta

#### **3. Ataques de Análisis Criptográfico**

- **Análisis de frecuencia**: Buscar patrones en el texto cifrado
- **Criptoanálisis diferencial**: Comparar diferencias en entrada/salida
- **Ataques de canal lateral**: Información de tiempo, energía, emanaciones electromagnéticas

---

## 3. Cifrado Simétrico 🔑

El cifrado simétrico es el método más antiguo e intuitivo. En el cifrado simétrico, **se utiliza la misma clave tanto para encriptar como para desencriptar** la información.

### ¿Cómo funciona?

```plaintext
Texto Plano + Clave → [Algoritmo] → Texto Cifrado
Texto Cifrado + Clave → [Algoritmo] → Texto Plano
```

1. **Acuerdo de Clave**: Ambas partes (emisor y receptor) deben tener acceso a la misma clave secreta de antemano.
2. **Cifrado**: El emisor utiliza el algoritmo de cifrado (ej. AES) y la clave secreta para convertir el texto plano en texto cifrado.
3. **Transmisión**: El texto cifrado se envía al receptor.
4. **Descifrado**: El receptor usa el mismo algoritmo y la misma clave secreta para revertir el proceso y obtener el texto plano original.

### Características Fundamentales

#### **✅ Ventajas**

- **Velocidad**: Extremadamente rápido y eficiente (1-15 GB/s en hardware moderno)
- **Eficiencia**: Bajo uso de CPU y memoria
- **Simplicidad**: Implementación más directa
- **Ideal para grandes volúmenes**: Streams de video, bases de datos completas, archivos grandes

#### **❌ Desventajas**

- **Distribución de la Clave**: El gran problema es: ¿cómo compartes la clave secreta de forma segura con el receptor?
- **Escalabilidad**: n usuarios requieren n(n-1)/2 claves únicas
- **No repudio**: No se puede probar quién envió el mensaje

### AES (Advanced Encryption Standard): El Estándar de Oro

AES es el estándar actual para el cifrado simétrico. Fue adoptado por el gobierno de EE. UU. en 2001 y hoy se usa globalmente.

#### **Características Técnicas de AES**

- **Longitud de clave**: 128, 192, o 256 bits
- **Tamaño de bloque**: 128 bits (16 bytes)
- **Rondas de cifrado**:
  - AES-128: 10 rondas
  - AES-192: 12 rondas  
  - AES-256: 14 rondas
- **Velocidad**: 1-15 GB/s (con aceleración hardware AES-NI)

#### **Funcionamiento Interno de AES**

Cada ronda de AES aplica cuatro operaciones:

```javascript
// Ejemplo conceptual de una ronda AES
function aesRound(state, roundKey) {
    state = subBytes(state);      // Sustitución no lineal (S-box)
    state = shiftRows(state);     // Desplazamiento cíclico de filas
    state = mixColumns(state);    // Multiplicación matricial (excepto última ronda)
    state = addRoundKey(state, roundKey); // XOR con clave de ronda
    return state;
}
```

1. **SubBytes**: Sustitución no lineal usando S-box (caja de sustitución)
2. **ShiftRows**: Desplazamiento cíclico de las filas del estado
3. **MixColumns**: Multiplicación matricial en el campo finito GF(2^8)
4. **AddRoundKey**: XOR con la clave de ronda correspondiente

### AES-256-GCM: El Estándar Moderno

Cuando ves "AES-256-GCM", se están describiendo tres elementos cruciales:

1. **AES**: El algoritmo base de cifrado por bloques
2. **256**: El tamaño de la clave en bits. Una clave de 256 bits significa 2^256 combinaciones posibles (un número astronómicamente grande)
3. **GCM (Galois/Counter Mode)**: El **modo de operación** del cifrador

#### **¿Por qué GCM es Superior?**

**GCM es un modo AEAD (Authenticated Encryption with Associated Data)**, lo que significa:

- **Confidencialidad**: Cifra los datos
- **Autenticidad**: Verifica el origen de los datos  
- **Integridad**: Detecta cualquier modificación
- **Paralelización**: Permite cifrado simultáneo de múltiples bloques

```javascript
// Node.js - Implementación AES-256-GCM
const crypto = require('crypto');

function encrypt(text, password) {
    const salt = crypto.randomBytes(32);
    const key = crypto.scryptSync(password, salt, 32); // Derivación segura de clave
    const nonce = crypto.randomBytes(12); // 96 bits para GCM
    
    const cipher = crypto.createCipher('aes-256-gcm');
    cipher.setAAD(Buffer.from('additional-data')); // Datos adicionales autenticados
    
    let encrypted = cipher.update(text, 'utf8', 'hex');
    encrypted += cipher.final('hex');
    const authTag = cipher.getAuthTag(); // Tag de autenticación
    
    return {
        encrypted,
        salt: salt.toString('hex'),
        nonce: nonce.toString('hex'),
        authTag: authTag.toString('hex')
    };
}

function decrypt(encryptedData, password) {
    const key = crypto.scryptSync(password, Buffer.from(encryptedData.salt, 'hex'), 32);
    
    const decipher = crypto.createDecipher('aes-256-gcm');
    decipher.setAAD(Buffer.from('additional-data'));
    decipher.setAuthTag(Buffer.from(encryptedData.authTag, 'hex'));
    
    let decrypted = decipher.update(encryptedData.encrypted, 'hex', 'utf8');
    decrypted += decipher.final('utf8');
    
    return decrypted;
}
```

### Modos de Operación Importantes

#### **1. ECB (Electronic Codebook) - ❌ NO USAR**

```plaintext
Bloque1 → AES → CifradoBloque1
Bloque2 → AES → CifradoBloque2
```

**Problema**: Patrones idénticos en el texto plano producen patrones idénticos en el texto cifrado.

#### **2. CBC (Cipher Block Chaining)**

```plaintext
Bloque1 ⊕ IV → AES → CifradoBloque1
Bloque2 ⊕ CifradoBloque1 → AES → CifradoBloque2
```

**Características**:

- Requiere Vector de Inicialización (IV) aleatorio
- Error se propaga al siguiente bloque
- No paralelizable para cifrado

#### **3. GCM (Galois/Counter Mode) - ✅ RECOMENDADO**

```plaintext
Counter+Nonce → AES → Keystream ⊕ Plaintext → Ciphertext + AuthTag
```

**Ventajas**:

- **AEAD**: Autenticación y cifrado simultáneo
- **Paralelizable**: Extremadamente rápido
- **Integridad**: Detecta modificaciones automáticamente
- **Nonce**: 96 bits, nunca se debe repetir con la misma clave

### Otros Algoritmos Simétricos

#### **ChaCha20-Poly1305**

- **Tipo**: Cifrado de flujo (stream cipher)
- **Ventaja**: Más rápido que AES en software puro (sin hardware especializado)
- **Clave**: 256 bits
- **Uso**: Ideal para móviles y dispositivos IoT

#### **DES y 3DES (Obsoletos)**

- **DES**: 56 bits de clave efectiva (roto desde 1997)
- **3DES**: Aplica DES tres veces (lento, en proceso de retirada)

> **En resumen:** **AES-256-GCM** es la opción preferida en la web moderna porque es increíblemente seguro, rápido y proporciona autenticación de datos de forma nativa. Es un pilar fundamental de TLS 1.2 y 1.3.

---

## 4. Cifrado Asimétrico 🔑-🔐

El cifrado asimétrico, también conocido como **criptografía de clave pública**, fue el gran avance que resolvió el problema de la distribución de claves del cifrado simétrico.

### Concepto Fundamental

En este sistema revolucionario, **se utiliza un par de claves matemáticamente relacionadas**:

```plaintext
Texto Plano + Clave Pública → [Algoritmo] → Texto Cifrado
Texto Cifrado + Clave Privada → [Algoritmo] → Texto Plano
```

- **Clave Pública**: Se puede compartir con cualquiera. Se usa para **encriptar** datos.
- **Clave Privada**: Debe mantenerse en secreto absoluto. Es la única que puede **desencriptar** los datos cifrados con su clave pública correspondiente.

### ¿Cómo funciona?

1. **Generación de Par de Claves**: El receptor (Bob) genera su propio par de claves (pública y privada).
2. **Distribución de Clave Pública**: Bob comparte su clave pública con el emisor (Alice) y con el mundo entero si quiere.
3. **Cifrado**: Alice usa la clave pública de Bob para encriptar el mensaje.
4. **Transmisión**: El texto cifrado se envía a Bob.
5. **Descifrado**: Bob usa su clave privada para descifrar el mensaje. Nadie más puede hacerlo.

### Características Fundamentales

#### **✅ Ventajas**

- **Intercambio Seguro de Claves**: Resuelve el problema de la distribución
- **Escalabilidad**: n usuarios solo necesitan n pares de claves
- **Autenticación**: Permite verificar identidades
- **No repudio**: Se puede probar quién envió un mensaje (firmas digitales)

#### **❌ Desventajas**

- **Lentitud**: 100-1000x más lento que el cifrado simétrico
- **Tamaño**: Claves y texto cifrado mucho más grandes
- **Complejidad**: Más propenso a errores de implementación

### RSA (Rivest-Shamir-Adleman): La Base Matemática

RSA es el algoritmo asimétrico más conocido. Su seguridad se basa en la **dificultad matemática de factorizar números grandes**.

#### **Funcionamiento Matemático Interno**

**1. Generación de Claves (El Secreto de los Primos):**

```python
# Paso 1: Elegir dos números primos gigantescos y distintos
p = 61  # Primo 1 (en realidad sería de 1024+ bits)
q = 53  # Primo 2

# Paso 2: Calcular el módulo público
n = p * q  # n = 3233 (se hace público)

# Paso 3: Calcular la función de Euler
phi_n = (p - 1) * (q - 1)  # φ(n) = 3120 (secreto)

# Paso 4: Elegir el exponente público
e = 17  # Debe ser coprimo con φ(n), comúnmente 65537

# Paso 5: Calcular el exponente privado
# d × e ≡ 1 (mod φ(n))
d = pow(e, -1, phi_n)  # d = 2753

# Claves resultantes:
# Clave Pública: (n=3233, e=17)
# Clave Privada: (n=3233, d=2753)
```

**2. Proceso de Cifrado y Descifrado:**

```python
def rsa_encrypt(message, e, n):
    # Convertir mensaje a número
    m = int.from_bytes(message.encode(), 'big')
    # Cifrar: c = m^e mod n
    c = pow(m, e, n)
    return c

def rsa_decrypt(ciphertext, d, n):
    # Descifrar: m = c^d mod n
    m = pow(ciphertext, d, n)
    # Convertir número a mensaje
    return m.to_bytes((m.bit_length() + 7) // 8, 'big').decode()
```

#### **¿Por qué funciona RSA?**

La matemática se basa en el **Teorema de Euler**:

- Si gcd(m, n) = 1, entonces m^φ(n) ≡ 1 (mod n)
- Por construcción: m^(e×d) ≡ m^1 ≡ m (mod n)
- Por tanto: (m^e)^d ≡ m (mod n)

#### **Seguridad y Longitudes de Clave**

**Basada en**:

- **Factorización de números primos**: La dificultad de factorizar un número entero grande (un semiprimo, que es el producto de dos números primos grandes) para garantizar la seguridad del cifrado.

- **Problema del logaritmo discreto**: La dificultad de este problema radica en que calcular k a partir de g y a es computacionalmente muy difícil para k grandes, lo que lo convierte en una herramienta fundamental en la criptografía moderna.

| Longitud | Estado | Uso Recomendado |
|----------|--------|-----------------|
| 1024 bits | ❌ Roto | No usar |
| 2048 bits | ⚠️ Mínimo | Sistemas legacy |
| 3072 bits | ✅ Seguro | Nuevos sistemas |
| 4096 bits | ✅ Máxima seguridad | Datos críticos |

#### **Limitaciones de RSA**

1. **Velocidad**: 100-1000x más lento que AES
2. **Tamaño**: Clave y cifrado mucho más grandes
3. **Quantum**: Vulnerable al algoritmo de Shor
4. **Implementación**: Fácil de implementar mal

### Curvas Elípticas (ECC): La Alternativa Moderna

#### **Ventajas sobre RSA**

- **Claves más cortas**: 256-bit ECC ≈ 3072-bit RSA en seguridad
- **Más rápido**: Especialmente en dispositivos móviles e IoT
- **Menos memoria**: Importante para sistemas embebidos

#### **Curvas Estándar**

- **P-256**: NIST estándar, ampliamente soportado
- **P-384**: Mayor seguridad para aplicaciones críticas
- **Curve25519**: Diseño moderno y rápido
- **Ed25519**: Optimizado para firmas digitales

### Firmas Digitales: Autenticidad e Integridad

Las firmas digitales invierten el uso de las claves asimétricas para probar la identidad del emisor.

**Proceso de Firma:**

1. El emisor calcula el **hash** del mensaje.
2. Cifra ese **hash** con su **clave privada**. El resultado es la **firma**.
3. Envía el mensaje original + la firma.

**Proceso de Verificación:**

1. El receptor calcula el **hash** del mensaje recibido.
2. Usa la **clave pública** del emisor para descifrar la firma y obtener el hash original.
3. Compara los dos hashes. Si coinciden, se prueba:
      - **Autenticidad**: El mensaje solo pudo ser firmado por el poseedor de la clave privada.
      - **Integridad**: El mensaje no fue alterado (de lo contrario, los hashes no coincidirían).

**En Resumen, Permiten verificar:**

- **Autenticidad**: Quién envió el mensaje
- **Integridad**: El mensaje no fue modificado
- **No repudio**: El emisor no puede negar haberlo enviado

#### **Proceso con RSA**

```python
import hashlib

# Firma (con clave privada)
def sign_message(message, d, n):
    # Hash del mensaje
    hash_msg = hashlib.sha256(message.encode()).digest()
    hash_int = int.from_bytes(hash_msg, 'big')
    # Firmar: signature = hash^d mod n
    signature = pow(hash_int, d, n)
    return signature

# Verificación (con clave pública)  
def verify_signature(message, signature, e, n):
    # Hash del mensaje recibido
    hash_msg = hashlib.sha256(message.encode()).digest()
    hash_int = int.from_bytes(hash_msg, 'big')
    # Verificar: hash_recovered = signature^e mod n
    hash_recovered = pow(signature, e, n)
    return hash_int == hash_recovered
```

---

## 5. Funciones Hash: La Huella Digital de los Datos

Una función hash criptográfica no es un algoritmo de encriptación, aunque a menudo se agrupan en discusiones de seguridad. A diferencia del cifrado, el hashing es un proceso **unidireccional** - no se puede "deshashear" un resultado para obtener la entrada original.

### Concepto Fundamental

Un hash toma una entrada de cualquier tamaño y produce una salida de tamaño fijo, llamada "resumen", "digest" o "hash".

```plaintext
Entrada (cualquier tamaño) → [Función Hash] → Salida (tamaño fijo)
"Hola Mundo" → [SHA-256] → "a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e"
```

### Propiedades Fundamentales

#### **1. Determinista**

- La misma entrada siempre produce la misma salida
- `hash("mensaje") = "abc123..."` (siempre)

#### **2. Eficiente**

- Calcular el hash de una entrada es rápido
- Velocidades de ~500 MB/s para SHA-256

#### **3. Resistencia a la Pre-imagen (Unidireccional)**

- A partir de un hash, es computacionalmente inviable encontrar la entrada original
- Dado `"abc123..."`, encontrar qué produjo este hash es imposible

#### **4. Resistencia a la Segunda Pre-imagen**

- Dada una entrada, es inviable encontrar otra entrada diferente que produzca el mismo hash
- Si `hash(entrada1) = "abc123..."`, encontrar `entrada2` donde `hash(entrada2) = "abc123..."` es imposible

#### **5. Resistencia a Colisiones**

- Es inviable encontrar dos entradas diferentes que produzcan el mismo hash
- `hash(entrada1) = hash(entrada2)` donde `entrada1 ≠ entrada2` debe ser imposible de encontrar

#### **6. Efecto Avalancha**

- Un pequeño cambio en la entrada causa un cambio drástico en la salida
- `SHA256("hello")` vs `SHA256("Hello")` → salidas completamente diferentes

> **Analogía 🧠:** Un hash es como una **huella digital** para los datos. Es única, fácil de tomar, pero es imposible reconstruir a la persona a partir de su huella. También se usa para verificar la **integridad**: si un solo bit del dato cambia, la huella digital (el hash) cambiará drásticamente.

### La Familia SHA (Secure Hash Algorithm)

SHA es una familia de funciones hash criptográficas diseñadas por la NSA y estandarizadas por el NIST.

#### **SHA-1 (160 bits) - ❌ OBSOLETO Y ROTO**

- **Estado**: Vulnerabilidades de colisión demostradas (2017)
- **Uso actual**: Solo para compatibilidad legacy (Git aún lo usa)
- **Recomendación**: No usar para aplicaciones nuevas. Reemplazar por SHA-256 o superior

#### **SHA-2 Family - ✅ ESTÁNDAR ACTUAL**

**SHA-256 (256 bits)**:

```javascript
const crypto = require('crypto');

function sha256(data) {
    return crypto.createHash('sha256')
                 .update(data)
                 .digest('hex');
}

// Ejemplos
console.log(sha256("Hello World"));
// Output: a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e

console.log(sha256("Hello Worlc")); // Un solo carácter diferente
// Output: completamente diferente debido al efecto avalancha
```

**Características de SHA-256**:

- **Longitud de salida**: 256 bits (64 caracteres hexadecimales)
- **Velocidad**: ~500 MB/s en hardware moderno
- **Seguridad**: 128 bits de seguridad contra ataques de colisión
- **Uso**: Bitcoin, certificados digitales, verificación de integridad

**SHA-512 (512 bits)**:

- **Mayor seguridad**: 256 bits de seguridad contra colisiones
- **Más rápido**: En procesadores de 64 bits
- **Uso**: Derivación de claves, aplicaciones de alta seguridad

#### **SHA-3 (Keccak) - ✅ ALTERNATIVA MODERNA**

- **Diseño**: Basado en "construcción de esponja" (diferente a SHA-2)
- **Propósito**: No fue creado porque SHA-2 estuviera roto, sino como alternativa robusta
- **Ventajas**: Mejor resistencia contra ataques de extensión de longitud
- **Estado**: Estándar desde 2015, pero menos adoptado que SHA-2
- **Variantes**: SHA3-224, SHA3-256, SHA3-384, SHA3-512

### Casos de Uso Principales

#### **1. Almacenamiento Seguro de Contraseñas**

**❌ NUNCA guardar contraseñas en texto plano, ni cifradas:** Se deben guardar *hasheadas*.

**Hashing Simple (INCORRECTO):**

```javascript
// MAL - Vulnerable a rainbow tables
const plainPassword = "miPassword123";
const badHash = sha256(plainPassword);
// Almacenar: "a1b2c3..."
```

**✅ Forma correcta:**

```javascript
const bcrypt = require('bcrypt');
const argon2 = require('argon2');

// Usando bcrypt
const saltRounds = 12;
const hashedPassword = await bcrypt.hash(password, saltRounds);

// Usando Argon2 (recomendado)
async function hashPassword(password) {
    // El salt se genera automáticamente
    return await argon2.hash(password, {
        type: argon2.argon2id, // La variante más resistente
        memoryCost: 2 ** 16,  // 64MB de memoria
        timeCost: 3,          // 3 iteraciones
        parallelism: 1,       // Grado de paralelismo
    });
}

async function verifyPassword(hash, password) {
    return await argon2.verify(hash, password);
}
```

**¿Por qué algoritmos especiales para contraseñas?**

- **SHA-256 es demasiado rápido**: Un atacante puede probar billones de combinaciones por segundo
- **Necesitamos algoritmos lentos**: bcrypt, scrypt, Argon2 están diseñados para ser costosos
  - Bcrypt: Un clásico muy robusto. Puede probar ~1000 contraseñas/segundo.
  - scrypt: Diseñado para ser intensivo en memoria.
  - Argon2: ✅ El estándar recomendado actualmente. Ganador de la Password Hashing Competition, es altamente resistente a ataques con hardware especializado (GPUs/ASICs).
- **Resistencia a hardware**: Argon2 usa mucha memoria, dificultando ataques con GPU/ASIC

#### **1.2. Mejorando el Hashing: Salt y Pepper**

**Salt (Sal)**: Cadena aleatoria única por cada usuario

```javascript
function hashPasswordWithSalt(password) {
    const salt = crypto.randomBytes(32); // 32 bytes aleatorios
    const combined = password + salt.toString('hex');
    const hash = sha256(combined);
    
    // Almacenar tanto el hash como el salt
    return {
        hash: hash,
        salt: salt.toString('hex')
    };
}

// Verificación
function verifyPassword(password, storedHash, storedSalt) {
    const combined = password + storedSalt;
    const calculatedHash = sha256(combined);
    return calculatedHash === storedHash;
}
```

**Pepper (Pimienta)**: Secreto global de la aplicación

```javascript
const APP_PEPPER = process.env.CRYPTO_PEPPER; // Variable de entorno

function hashPasswordWithSaltAndPepper(password, salt) {
    const combined = password + salt + APP_PEPPER;
    return sha256(combined);
}
```

**Beneficios combinados**:

- **Salt**: Previene ataques de rainbow tables y hace únicos hashes de contraseñas iguales
- **Pepper**: Añade protección incluso si la base de datos es comprometida

#### **2. Verificación de Integridad de Archivos (Checksums)**

Un **checksum** es esencialmente una "huella digital" de un archivo:

```bash
# Generar checksum
echo "Contenido del archivo" > archivo.txt
sha256sum archivo.txt
# Output: f1d2d2f924e986ac86fdf7b36c94bcdf32beec15 archivo.txt

# Verificar integridad
echo "f1d2d2f924e986ac86fdf7b36c94bcdf32beec15 archivo.txt" | sha256sum -c
# Output: archivo.txt: OK
```

**Proceso de verificación**:

1. El origen calcula y publica el hash del archivo
2. Tú descargas el archivo
3. Calculas el hash de tu copia local
4. Comparas ambos hashes
5. **Si coinciden**: Archivo íntegro ✅
6. **Si difieren**: Archivo corrupto o manipulado ❌

> **Analogía del Sello de Cera 📜:** Como un rey medieval que sella un pergamino con cera y su anillo. Si el sello está intacto, el mensaje no fue alterado.

#### **3. HMAC (Hash-based Message Authentication Code)**

HMAC proporciona **autenticación** e **integridad** usando una clave secreta:

```javascript
const crypto = require('crypto');

function createHMAC(message, secretKey) {
    return crypto.createHmac('sha256', secretKey)
                 .update(message)
                 .digest('hex');
}

// Crear HMAC
const secret = "mi-clave-secreta";
const message = "Mensaje importante";
const hmac = createHMAC(message, secret);

// Verificar HMAC
function verifyHMAC(message, hmac, secretKey) {
    const calculatedHMAC = createHMAC(message, secretKey);
    return calculatedHMAC === hmac;
}

// El cliente envía: payload (mensaje) + signature (hmac)
// El servidor verifica que el payload no fue modificado
const isValid = verifyHMAC(secret, message, hmac);
```

**Usos de HMAC**:

- **JWT signatures**: Verificar que un token no fue modificado
- **API authentication**: Firmar peticiones para verificar origen
- **Webhooks**: Verificar que un webhook proviene del servicio correcto

#### **4. Proof of Work (Blockchain)**

**Ejemplo:**

```javascript
function mineBlock(data, difficulty) {
    let nonce = 0;
    let hash;
    const target = "0".repeat(difficulty); // Ej: "0000"
    
    console.log(`Minando bloque con dificultad ${difficulty}...`);
    
    do {
        const blockData = data + nonce;
        hash = sha256(blockData);
        nonce++;
        
        if (nonce % 100000 === 0) {
            console.log(`Intentos: ${nonce}, Hash: ${hash}`);
        }
    } while (!hash.startsWith(target));
    
    console.log(`¡Bloque minado! Nonce: ${nonce - 1}, Hash: ${hash}`);
    return { hash, nonce: nonce - 1 };
}

// Ejemplo: encontrar hash que empiece con "0000"
const result = mineBlock("Transaction: Alice -> Bob: 10 BTC", 4);
```

### Comparación de Algoritmos Hash

| Algoritmo | Tipo | Velocidad | Seguridad | Uso Principal |
| :--- | :--- | :---: | :---: | :--- |
| **AES-256-GCM** | Simétrico | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Cifrado de datos en tránsito (TLS) y en reposo. |
| **ChaCha20-Poly1305** | Simétrico | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Dispositivos móviles, IoT, software sin aceleración AES. |
| **RSA-3072** | Asimétrico | ⭐⭐ | ⭐⭐⭐⭐ | Firmas digitales y certificados (PKI). |
| **X25519 (ECC)** | Asimétrico | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Intercambio de claves (ECDH). El estándar en TLS 1.3. |
| **Ed25519 (ECC)** | Asimétrico | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Firmas digitales modernas. Más rápido y seguro que RSA. |
| **Argon2id** | Hash (KDF) | ⭐ | ⭐⭐⭐⭐⭐ | Almacenamiento de contraseñas. **Lento por diseño**. |
| **SHA-256** | Hash | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Firmas, integridad de archivos (checksums), blockchain. |

---

## 6. Casos de Uso en la Web

La web moderna combina cifrado simétrico y asimétrico en un **esquema híbrido**. Así funciona **HTTPS (TLS/SSL)**:

1. **Handshake TLS**: Navegador se conecta al servidor
2. **Intercambio de Certificado**: Servidor envía su clave pública (en el certificado)
3. **Generación de Clave de Sesión**: Navegador genera una clave simétrica aleatoria
4. **Cifrado Asimétrico**: Navegador cifra la clave de sesión con la clave pública del servidor
5. **Intercambio Seguro**: Clave de sesión cifrada se envía al servidor
6. **Descifrado**: Servidor descifra la clave de sesión con su clave privada
7. **Comunicación Simétrica**: Todo el tráfico posterior usa cifrado simétrico (rápido)

```plaintext
Cliente                              Servidor
  |--- ClientHello ------------------>|
  |<-- ServerHello + Certificate -----|
  |--- ClientKeyExchange ------------>| (clave simétrica cifrada con RSA)
  |<-- Finished ----------------------|
  |--- Finished --------------------->|
  |===== Datos con AES-256-GCM =======|
```

Este enfoque híbrido nos da la **seguridad** del intercambio asimétrico y la **velocidad** del cifrado simétrico.

### **Resumen Comunicación de datos:**

- Se genera clave simétrica temporal (AES-256)
- Se intercambia usando RSA/ECC (lento, una sola vez)
- Toda la comunicación posterior usa AES-256-GCM (rápido)

---

## 7. Análisis Comparativo de Rendimiento

### Algoritmos Simétricos

#### **AES vs ChaCha20: Rendimiento Detallado por Hardware**

**Datos de rendimiento** basados en implementaciones OpenSSL 3.0+, RFC 7539 y benchmarks de Cloudflare:

```plaintext
Hardware/Contexto               | AES-256-GCM     | ChaCha20-Poly1305 | Factor Ventaja
================================================================================
Intel con AES-NI (servidor)     | 8-15 GB/s      | 1.5-2.5 GB/s     | AES 5-6x más rápido
ARM64 con Crypto Extensions      | 2.5-5 GB/s     | 1.2-2 GB/s       | AES 2-3x más rápido
Software puro x86-64            | 150-300 MB/s   | 500-800 MB/s     | ChaCha20 2-3x más rápido
ARM32 (móviles sin crypto ext)   | 25-75 MB/s     | 75-200 MB/s      | ChaCha20 3-4x más rápido
JavaScript (V8/SpiderMonkey)     | 15-50 MB/s     | 100-200 MB/s     | ChaCha20 4-6x más rápido
Microcontroladores (32-bit)     | 1-8 MB/s       | 8-25 MB/s        | ChaCha20 5-8x más rápido
```

#### **Análisis Técnico de Rendimiento**

**¿Por qué AES es más rápido con aceleración hardware?**

- **AES-NI (Intel/AMD)**: Instrucciones dedicadas (`AESENC`, `AESENCLAST`) ejecutan una ronda completa en 1-2 ciclos
- **ARM Crypto Extensions**: Instrucciones `AESE`/`AESMC` proporcionan aceleración similar
- **Sin aceleración**: AES requiere operaciones costosas en tablas de sustitución (S-boxes) vulnerables a ataques de cache

**¿Por qué ChaCha20 domina en software puro?**

- **Operaciones ARX**: Solo usa sumas, rotaciones y XOR (primitivas muy eficientes en CPU)
- **Sin tablas**: Elimina accesos costosos a memoria y ataques de timing
- **Paralelización**: Fácil optimización con SIMD (SSE/AVX en x86, NEON en ARM)

#### **Consideraciones de Seguridad**

**AES-256-GCM**:

- **Fortaleza**: 256 bits de seguridad simétrica
- **Vulnerabilidades**: Ataques de timing en implementaciones software

**ChaCha20-Poly1305**:

- **Fortaleza**: 256 bits de seguridad simétrica
- **Ventajas**: Resistente a ataques de timing por diseño
- **Autenticación**: Poly1305 proporciona ~100 bits de seguridad de autenticación

#### **¿Cuándo usar cada algoritmo?**

**AES-256-GCM - Óptimo para:**

- **Servidores Intel/AMD modernos** (post-2010 con AES-NI)
- **ARM64 con extensiones crypto** (iPhone 5s+, servidores ARM modernas)
- **Máximo throughput** cuando hay aceleración hardware
- **Compatibilidad universal** (soportado en todo hardware/software)
- **Cumplimiento normativo** (certificado FIPS 140-2, aprobado por NSA)

**ChaCha20-Poly1305 - Óptimo para:**

- **Dispositivos móviles antiguos** (ARM32 sin crypto extensions)
- **Microcontroladores e IoT** (ESP32, Arduino, etc.)
- **Navegadores web** (JavaScript, WebAssembly)
- **Sistemas embebidos** sin aceleración criptográfica
- **Implementaciones críticas** donde se requiere resistencia a timing attacks
- **Software que prioriza simplicidad** de implementación segura

### Algoritmos Asimétricos

#### **RSA vs ECC: La Batalla por la Eficiencia**

```plaintext
Operación/Algoritmo        | RSA-2048    | RSA-3072    | ECDSA P-256 | Ed25519
========================================================================
Generación de Claves       | 20-100 ms   | 200-500 ms  | 1-5 ms      | 0.5-2 ms
Firma Digital              | 1-10 ms     | 5-20 ms     | 0.2-1 ms    | 0.1-0.5 ms
Verificación de Firma      | 0.1-0.5 ms  | 0.2-1 ms    | 0.5-2 ms    | 0.2-1 ms
Intercambio de Claves      | N/A         | N/A         | 0.5-2 ms    | 0.3-1 ms
Tamaño Clave Pública       | 256 bytes   | 384 bytes   | 64 bytes    | 32 bytes
Tamaño Clave Privada       | 1024 bytes  | 1536 bytes  | 32 bytes    | 32 bytes
Tamaño de Firma            | 256 bytes   | 384 bytes   | 64 bytes    | 64 bytes
```

#### **Niveles de Seguridad Equivalentes**

```plaintext
Bits de Seguridad | RSA        | ECC        | Factor de Mejora
=====================================================
80 bits           | 1024 bits  | 160 bits   | 6.4x más pequeño
112 bits          | 2048 bits  | 224 bits   | 9.1x más pequeño
128 bits          | 3072 bits  | 256 bits   | 12x más pequeño
192 bits          | 7680 bits  | 384 bits   | 20x más pequeño
256 bits          | 15360 bits | 512 bits   | 30x más pequeño
```

#### **¿Cuándo usar RSA vs ECC?**

**RSA - Ideal para:**

- Sistemas legacy que requieren compatibilidad máxima
- Cuando se necesita cifrado directo de datos pequeños
- Entornos donde ECC no está disponible
- Aplicaciones con restricciones de patentes (aunque la mayoría han expirado)

**ECC (ECDSA/Ed25519) - Ideal para:**

- Nuevos sistemas que priorizan rendimiento
- Dispositivos con recursos limitados (IoT, móviles)
- Aplicaciones que requieren alta velocidad de firma
- Protocolos modernos (TLS 1.3, SSH, Bitcoin)
- Sistemas con restricciones de ancho de banda

---

## 8. Cifrado en Reposo vs Cifrado en tránsito

En el ecosistema de seguridad digital, los datos necesitan protección en **dos estados fundamentales**: cuando están siendo **transmitidos** (en tránsito) y cuando están **almacenados** (en reposo). Cada escenario presenta desafíos únicos y requiere estrategias criptográficas específicas.

### Conceptos Fundamentales

#### **Cifrado en Tránsito (Data in Transit)**

Es la protección de datos mientras **se mueven** a través de redes, desde un punto de origen hasta un destino.

```plaintext
Cliente → [Internet/Red] → Servidor
   ↓            ↓            ↓
Datos       Interceptación   Datos
Planos      Posible (MITM)   Planos
```

**Escenarios típicos:**

- Navegación web (HTTPS)
- Transferencia de archivos (SFTP, SCP)
- Comunicación entre servicios (APIs, microservicios)
- Emails y mensajería instantánea
- Streaming de video/audio

#### **Cifrado en Reposo (Data at Rest)**

Es la protección de datos mientras están **almacenados** en sistemas de persistencia.

```plaintext
Aplicación → [Almacenamiento] → Recuperación
     ↓              ↓               ↓
  Datos          Acceso No        Datos
  Planos        Autorizado        Planos
```

**Escenarios típicos:**

- Bases de datos
- Archivos en discos duros/SSD
- Respaldos (backups)
- Almacenamiento en la nube
- Dispositivos móviles y laptops

### Comparación Técnica Detallada

#### **Diferencias Arquitecturales**

| Aspecto | Cifrado en Tránsito | Cifrado en Reposo |
|---------|-------------------|-------------------|
| **Duración** | Temporal (segundos/minutos) | Permanente (días/años) |
| **Alcance** | Punto a punto | Local/Centralizado |
| **Amenazas** | Intercepción, MITM | Robo físico, acceso no autorizado |
| **Rendimiento** | Crítico (latencia) | Menos crítico (throughput) |
| **Gestión de Claves** | Ephemeral keys (PFS) | Claves persistentes |
| **Algoritmos** | Híbridos (RSA+AES) | Principalmente simétricos |

#### **Vectores de Ataque Específicos**

**En Tránsito:**

- **Man-in-the-Middle (MITM)**: Interceptación activa
- **Packet Sniffing**: Captura pasiva de tráfico
- **DNS Spoofing**: Redirección maliciosa
- **Certificate Pinning Bypass**: Ataques a la validación de certificados
- **Downgrade Attacks**: Forzar protocolos menos seguros

**En Reposo:**

- **Physical Theft**: Robo de dispositivos/servidores
- **Insider Threats**: Acceso malicioso interno
- **Database Breaches**: Comprometimiento de SGBD
- **Backup Exposure**: Respaldos no cifrados
- **Cloud Misconfiguration**: Configuración incorrecta de permisos

### Mejores Prácticas por Escenario

#### **Para Cifrado en Tránsito:**

1. **Usar TLS 1.3** como mínimo, deshabilitando versiones anteriores
2. **Implementar HSTS** con preload para forzar HTTPS
3. **Certificate Pinning** en aplicaciones móviles críticas
4. **Perfect Forward Secrecy** con intercambio X25519
5. **Validación estricta de certificados** sin excepciones
6. **Monitoreo de conexiones** para detectar downgrade attacks

#### **Para Cifrado en Reposo:**

1. **Cifrado a múltiples niveles**: filesystem + database + application
2. **Rotación automática de claves** cada 90 días máximo
3. **Separación de claves**: datos y claves en sistemas diferentes
4. **Hardware Security Modules (HSM)** para claves críticas
5. **Cifrado de backups** con claves independientes
6. **Auditoría de acceso** a datos cifrados

### Consideraciones de Rendimiento

#### **Impacto en Tránsito:**

```javascript
// Benchmark de overhead criptográfico
const benchmark = {
    plainHTTP: {
        latency: '50ms',
        throughput: '1 GB/s',
        cpu: '5%'
    },
    httpsAES: {
        latency: '52ms',    // +4% overhead
        throughput: '950 MB/s', // -5% overhead  
        cpu: '8%'           // +60% overhead
    },
    httpsChaCha20: {
        latency: '53ms',    // +6% overhead
        throughput: '900 MB/s', // -10% overhead
        cpu: '12%'          // +140% overhead (sin AES-NI)
    }
};
```

#### **Impacto en Reposo:**

```javascript
const storageImpact = {
    plaintext: {
        size: '1 GB',
        readTime: '100ms',
        writeTime: '150ms'
    },
    encrypted: {
        size: '1.02 GB',    // +2% overhead (metadata)
        readTime: '105ms',  // +5% overhead
        writeTime: '160ms'  // +7% overhead
    }
};
```

**Optimizaciones recomendadas:**

- **Cachear sesiones TLS** para reducir handshakes
- **Usar hardware acceleration** (AES-NI) cuando esté disponible
- **Cifrado asíncrono** para no bloquear I/O
- **Compression antes del cifrado** para reducir tamaño
- **Cifrado selectivo** solo de datos verdaderamente sensibles

### Cumplimiento Normativo

#### **Requerimientos por Industria:**

| Industria | Estándar | Tránsito | Reposo | Algoritmos Requeridos |
|-----------|----------|----------|--------|--------------------|
| **Financiera** | PCI DSS | TLS 1.2+ | AES-256 | RSA-2048+, AES-256-GCM |
| **Salud** | HIPAA | TLS 1.2+ | AES-256 | FIPS 140-2 Level 3+ |
| **Gobierno** | FIPS 140-2 | Suite B | Suite B | NSA Suite B |
| **Europa** | GDPR | "Estado del arte" | "Estado del arte" | Recomendaciones ENISA |

---

## 9. Patrones de Seguridad Web Aplicados

Ahora unamos todo el conocimiento teórico con la implementación práctica. ¿Cómo se manifiestan estos conceptos en el día a día de un desarrollador Full Stack?

<!-- TODO: Refinar el contenido de los Pattern. -->

### Pattern 1: Asegurar Datos en Tránsito (HTTPS/TLS)

#### **El Protocolo TLS 1.3: Handshake Optimizado**

```plaintext
Cliente                              Servidor
  |--- ClientHello ------------------>|
  |    (cipher suites, key shares)    |
  |                                   |
  |<-- ServerHello -------------------|  
  |    (selected cipher, key share)   |
  |<-- {EncryptedExtensions} ---------|
  |<-- {Certificate} -----------------|
  |<-- {CertificateVerify} -----------|
  |<-- {Finished} -------------------|
  |                                   |
  |--- {Finished} ------------------>|
  |                                   |
  |===== Datos con AES-256-GCM =======|
```

**Tecnologías utilizadas**:

- **Intercambio de claves**: X25519 (ECDH) o RSA-4096
- **Autenticación**: Ed25519, ECDSA P-384, o RSA-PSS
- **Cifrado simétrico**: AES-256-GCM o ChaCha20-Poly1305
- **Hash**: SHA-256 o SHA-384

#### **Configuración Nginx Segura (2024)**

```nginx
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    
    # Certificados
    ssl_certificate /path/to/fullchain.pem;
    ssl_certificate_key /path/to/private.key;
    
    # Protocolos seguros únicamente
    ssl_protocols TLSv1.2 TLSv1.3;
    
    # Cipher suites modernas
    ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305;
    ssl_prefer_server_ciphers off;
    
    # Curvas elípticas seguras
    ssl_ecdh_curve X25519:prime256v1:secp384r1;
    
    # HSTS (HTTP Strict Transport Security)
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
    
    # OCSP Stapling para verificación de certificados
    ssl_stapling on;
    ssl_stapling_verify on;
    ssl_trusted_certificate /path/to/chain.pem;
    
    # Configuraciones adicionales de seguridad
    add_header X-Frame-Options DENY always;
    add_header X-Content-Type-Options nosniff always;
    add_header Referrer-Policy strict-origin-when-cross-origin always;
    add_header Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline';" always;
}
```

### Pattern 2: Asegurar Datos en Reposo (Bases de Datos y Archivos)

#### **Sistema Completo de Gestión de Contraseñas**

```javascript
const argon2 = require('argon2');
const crypto = require('crypto');

class SecurePasswordManager {
    constructor() {
        this.pepper = process.env.CRYPTO_PEPPER;
        if (!this.pepper) {
            throw new Error('CRYPTO_PEPPER environment variable required');
        }
    }
    
    /**
     * Hash una contraseña con salt y pepper
     */
    async hashPassword(password) {
        // Generar salt único para este usuario
        const salt = crypto.randomBytes(32);
        
        // Combinar password + salt + pepper
        const combined = password + salt.toString('hex') + this.pepper;
        
        // Usar Argon2id con configuración robusta
        const hash = await argon2.hash(combined, {
            type: argon2.argon2id,
            memoryCost: 2 ** 16,    // 64MB de memoria
            timeCost: 3,            // 3 iteraciones
            parallelism: 1,         // 1 hilo
            hashLength: 32          // 256 bits de salida
        });
        
        return {
            hash,
            salt: salt.toString('hex'),
            algorithm: 'argon2id',
            params: { memoryCost: 65536, timeCost: 3, parallelism: 1 }
        };
    }
    
    /**
     * Verificar contraseña
     */
    async verifyPassword(password, storedHash, storedSalt) {
        const combined = password + storedSalt + this.pepper;
        
        try {
            return await argon2.verify(storedHash, combined);
        } catch (err) {
            // Log del intento fallido para detección de ataques
            console.error('Password verification failed:', err);
            return false;
        }
    }
    
    /**
     * Verificar si el hash necesita actualizarse (rehashing)
     */
    needsRehash(storedHash) {
        return argon2.needsRehash(storedHash, {
            type: argon2.argon2id,
            memoryCost: 2 ** 16,
            timeCost: 3,
            parallelism: 1
        });
    }
}
```

#### **Modelo de Usuario con Cifrado de Datos Sensibles**

```javascript
const crypto = require('crypto');

class SecureUserModel {
    constructor(encryptionKey) {
        this.key = Buffer.from(encryptionKey, 'hex');
        this.algorithm = 'aes-256-gcm';
    }
    
    /**
     * Cifrar datos sensibles (PII)
     */
    encryptPII(data) {
        const nonce = crypto.randomBytes(12); // 96 bits para GCM
        const cipher = crypto.createCipher(this.algorithm);
        cipher.setAAD(Buffer.from('user-pii-encryption'));
        
        let encrypted = cipher.update(JSON.stringify(data), 'utf8', 'hex');
        encrypted += cipher.final('hex');
        const authTag = cipher.getAuthTag();
        
        return {
            data: encrypted,
            nonce: nonce.toString('hex'),
            authTag: authTag.toString('hex'),
            algorithm: this.algorithm
        };
    }
    
    /**
     * Descifrar datos sensibles
     */
    decryptPII(encryptedData) {
        const decipher = crypto.createDecipher(this.algorithm);
        decipher.setAAD(Buffer.from('user-pii-encryption'));
        decipher.setAuthTag(Buffer.from(encryptedData.authTag, 'hex'));
        
        let decrypted = decipher.update(encryptedData.data, 'hex', 'utf8');
        decrypted += decipher.final('utf8');
        
        return JSON.parse(decrypted);
    }
    
    /**
     * Crear usuario con datos cifrados
     */
    async createUser(userData) {
        const passwordManager = new SecurePasswordManager();
        
        // Hash de la contraseña
        const passwordData = await passwordManager.hashPassword(userData.password);
        
        // Cifrar datos sensibles
        const sensitiveData = {
            fullName: userData.fullName,
            dateOfBirth: userData.dateOfBirth,
            ssn: userData.ssn,
            address: userData.address
        };
        const encryptedPII = this.encryptPII(sensitiveData);
        
        // Datos públicos (no cifrados)
        const publicData = {
            id: crypto.randomUUID(),
            email: userData.email,
            username: userData.username,
            createdAt: new Date().toISOString(),
            lastLogin: null
        };
        
        return {
            ...publicData,
            passwordHash: passwordData.hash,
            passwordSalt: passwordData.salt,
            encryptedData: encryptedPII
        };
    }
}
```

### Pattern 3: Autenticación y Autorización con JWT

#### **Implementación JWT Segura con Rotación de Tokens**

```javascript
const jwt = require('jsonwebtoken');
const crypto = require('crypto');

class SecureJWTManager {
    constructor() {
        this.accessTokenSecret = process.env.JWT_ACCESS_SECRET;
        this.refreshTokenSecret = process.env.JWT_REFRESH_SECRET;
        this.accessTokenExpiry = '15m';
        this.refreshTokenExpiry = '7d';
        
        // Redis o base de datos para blacklist
        this.tokenBlacklist = new Set();
    }
    
    /**
     * Generar par de tokens (access + refresh)
     */
    generateTokenPair(userId, userRole, sessionId = null) {
        const sessionIdentifier = sessionId || crypto.randomUUID();
        const currentTime = Math.floor(Date.now() / 1000);
        
        // Access Token (corto, con permisos)
        const accessPayload = {
            sub: userId,                    // Subject (user ID)
            role: userRole,                 // Role-based permissions
            session: sessionIdentifier,     // Session identifier
            type: 'access',                 // Token type
            iat: currentTime,              // Issued at
            aud: 'my-app-users'            // Audience
        };
        
        const accessToken = jwt.sign(
            accessPayload,
            this.accessTokenSecret,
            { 
                algorithm: 'HS256',
                expiresIn: this.accessTokenExpiry,
                issuer: 'my-app-auth-service'
            }
        );
        
        // Refresh Token (largo, solo para renovación)
        const refreshPayload = {
            sub: userId,
            session: sessionIdentifier,
            type: 'refresh',
            iat: currentTime,
            aud: 'my-app-refresh'
        };
        
        const refreshToken = jwt.sign(
            refreshPayload,
            this.refreshTokenSecret,
            {
                algorithm: 'HS256',
                expiresIn: this.refreshTokenExpiry,
                issuer: 'my-app-auth-service'
            }
        );
        
        return {
            accessToken,
            refreshToken,
            sessionId: sessionIdentifier,
            expiresIn: 900 // 15 minutos en segundos
        };
    }
    
    /**
     * Verificar y renovar access token usando refresh token
     */
    async refreshAccessToken(refreshToken) {
        try {
            // Verificar refresh token
            const decoded = jwt.verify(refreshToken, this.refreshTokenSecret, {
                algorithms: ['HS256'],
                issuer: 'my-app-auth-service',
                audience: 'my-app-refresh'
            });
            
            // Validaciones adicionales
            if (decoded.type !== 'refresh') {
                throw new Error('Invalid token type');
            }
            
            // Verificar que no esté en blacklist
            if (await this.isTokenBlacklisted(refreshToken)) {
                throw new Error('Token has been revoked');
            }
            
            // Obtener información actualizada del usuario
            const user = await this.getUserById(decoded.sub);
            if (!user || !user.active) {
                throw new Error('User not found or inactive');
            }
            
            // Generar nuevo par de tokens
            return this.generateTokenPair(
                decoded.sub, 
                user.role, 
                decoded.session
            );
            
        } catch (error) {
            throw new Error(`Token refresh failed: ${error.message}`);
        }
    }
    
    /**
     * Verificar access token
     */
    verifyAccessToken(accessToken) {
        try {
            const decoded = jwt.verify(accessToken, this.accessTokenSecret, {
                algorithms: ['HS256'],
                issuer: 'my-app-auth-service',
                audience: 'my-app-users'
            });
            
            if (decoded.type !== 'access') {
                throw new Error('Invalid token type');
            }
            
            return decoded;
        } catch (error) {
            throw new Error(`Token verification failed: ${error.message}`);
        }
    }
    
    /**
     * Revocar token (agregar a blacklist)
     */
    async revokeToken(token) {
        this.tokenBlacklist.add(token);
        // En producción, guardar en Redis con TTL igual al tiempo restante del token
        const decoded = jwt.decode(token);
        const ttl = decoded.exp - Math.floor(Date.now() / 1000);
        // redis.setex(token, ttl, 'revoked');
    }
    
    /**
     * Verificar si token está en blacklist
     */
    async isTokenBlacklisted(token) {
        return this.tokenBlacklist.has(token);
        // En producción: return await redis.exists(token);
    }
    
    /**
     * Cerrar todas las sesiones de un usuario
     */
    async revokeAllUserTokens(userId) {
        // Implementar lógica para invalidar todos los tokens de un usuario
        // Esto requiere mantener un registro de sesiones activas
    }
}
```

### Pattern 4: Verificación de Integridad Avanzada

#### **Sistema de Verificación de Integridad de Archivos con Metadatos**

```javascript
const crypto = require('crypto');
const fs = require('fs').promises;

class FileIntegrityManager {
    constructor() {
        this.algorithm = 'sha256';
        this.blockSize = 1024 * 1024; // 1MB bloques para archivos grandes
    }
    
    /**
     * Calcular hash de archivo con metadatos
     */
    async calculateFileFingerprint(filePath) {
        try {
            const stats = await fs.stat(filePath);
            const fileHandle = await fs.open(filePath, 'r');
            
            // Hash del contenido
            const contentHash = crypto.createHash(this.algorithm);
            const buffer = Buffer.alloc(this.blockSize);
            let position = 0;
            
            while (position < stats.size) {
                const { bytesRead } = await fileHandle.read(buffer, 0, this.blockSize, position);
                if (bytesRead === 0) break;
                
                contentHash.update(buffer.subarray(0, bytesRead));
                position += bytesRead;
            }
            
            await fileHandle.close();
            
            // Crear fingerprint completo
            const fingerprint = {
                contentHash: contentHash.digest('hex'),
                size: stats.size,
                lastModified: stats.mtime.toISOString(),
                algorithm: this.algorithm,
                timestamp: new Date().toISOString()
            };
            
            // Hash del fingerprint completo
            const metaHash = crypto.createHash(this.algorithm)
                .update(JSON.stringify(fingerprint))
                .digest('hex');
            
            return {
                ...fingerprint,
                metaHash
            };
            
        } catch (error) {
            throw new Error(`Failed to calculate file fingerprint: ${error.message}`);
        }
    }
    
    /**
     * Verificar integridad de archivo
     */
    async verifyFileIntegrity(filePath, expectedFingerprint) {
        const currentFingerprint = await this.calculateFileFingerprint(filePath);
        
        const verification = {
            isValid: currentFingerprint.contentHash === expectedFingerprint.contentHash,
            sizeMatches: currentFingerprint.size === expectedFingerprint.size,
            hashMatches: currentFingerprint.contentHash === expectedFingerprint.contentHash,
            currentHash: currentFingerprint.contentHash,
            expectedHash: expectedFingerprint.contentHash,
            sizeChanged: currentFingerprint.size !== expectedFingerprint.size,
            timeChanged: currentFingerprint.lastModified !== expectedFingerprint.lastModified
        };
        
        return verification;
    }
    
    /**
     * Generar checksum para múltiples archivos
     */
    async generateManifest(filesList) {
        const manifest = {
            created: new Date().toISOString(),
            algorithm: this.algorithm,
            files: {}
        };
        
        for (const filePath of filesList) {
            try {
                manifest.files[filePath] = await this.calculateFileFingerprint(filePath);
            } catch (error) {
                manifest.files[filePath] = { error: error.message };
            }
        }
        
        // Hash del manifest completo
        manifest.manifestHash = crypto.createHash(this.algorithm)
            .update(JSON.stringify(manifest.files))
            .digest('hex');
        
        return manifest;
    }
    
    /**
     * Verificar integridad usando manifest
     */
    async verifyManifest(filesList, manifest) {
        const results = {
            overallValid: true,
            fileResults: {},
            summary: {
                total: filesList.length,
                valid: 0,
                invalid: 0,
                missing: 0
            }
        };
        
        for (const filePath of filesList) {
            if (!manifest.files[filePath]) {
                results.fileResults[filePath] = { status: 'not_in_manifest' };
                results.summary.missing++;
                results.overallValid = false;
                continue;
            }
            
            try {
                const verification = await this.verifyFileIntegrity(
                    filePath, 
                    manifest.files[filePath]
                );
                
                results.fileResults[filePath] = verification;
                
                if (verification.isValid) {
                    results.summary.valid++;
                } else {
                    results.summary.invalid++;
                    results.overallValid = false;
                }
            } catch (error) {
                results.fileResults[filePath] = { status: 'error', error: error.message };
                results.summary.invalid++;
                results.overallValid = false;
            }
        }
        
        return results;
    }
}

// Uso práctico
const integrityManager = new FileIntegrityManager();

// Crear manifest de archivos críticos
const criticalFiles = [
    '/app/config/production.json',
    '/app/dist/bundle.js',
    '/app/package.json'
];

const manifest = await integrityManager.generateManifest(criticalFiles);

// Verificar integridad posteriormente
const verification = await integrityManager.verifyManifest(criticalFiles, manifest);
console.log('Integrity Check:', verification.overallValid ? 'PASSED' : 'FAILED');
```

Estos patrones forman la base de un sistema de seguridad robusto en aplicaciones web modernas, combinando la teoría criptográfica con implementaciones prácticas y seguras.

## 10. Buenas Prácticas y Resumen

- **Nunca implementes tu propia criptografía**. Usa librerías estándar, auditadas y bien mantenidas (`libsodium`, `OpenSSL`, y las APIs nativas de tu lenguaje como `crypto` en Node.js).
- **Mantén las claves seguras**. Las claves son el eslabón más débil. Usa gestores de secretos (Vault, KMS) y nunca las hardcodees en tu código.
- **Usa los algoritmos correctos para el trabajo correcto**:
  - **Contraseñas**: `Argon2id`.
  - **Datos en tránsito/reposo**: `AES-256-GCM`.
  - **Firmas digitales**: `Ed25519` (o `RSA-3072` si es necesario).
- **Mantente actualizado**. El campo de la criptografía evoluciona. Algoritmos que son seguros hoy pueden ser débiles mañana. Sigue las recomendaciones de organizaciones como NIST y OWASP.
