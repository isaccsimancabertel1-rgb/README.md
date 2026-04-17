# 🔐 Encriptación y Seguridad Informática

## 📄 Descripción

Este proyecto tiene como objetivo explicar la importancia de la seguridad informática y demostrar, mediante un ejemplo en Python, cómo funciona la encriptación de datos.

Se busca proteger la información frente a accesos no autorizados, mostrando conceptos básicos como cifrado, claves y validación de acceso.

---

## 🎯 Objetivo

Comprender la importancia de la encriptación en la seguridad informática, identificando sus conceptos básicos y aplicándolos en un programa que protege un mensaje mediante una clave secreta.

---

## 🧠 Conceptos Teóricos

### 🔑 Encriptación

Es el proceso de convertir un mensaje legible en un formato ilegible utilizando una clave, con el fin de proteger la información.

### 🔐 Tipos de Encriptación

* **Cifrado Simétrico**: Usa una sola clave para encriptar y desencriptar.
* **Cifrado Asimétrico (RSA)**: Usa dos claves (pública y privada).
* **Funciones Hash**: Transforman datos en un valor único que no se puede revertir.

### 🌐 Seguridad Informática

Es la disciplina encargada de proteger la información y los sistemas frente a accesos no autorizados.

Se divide en:

* Seguridad de hardware
* Seguridad de software
* Seguridad de red

---

## ⚙️ Implementación

El programa implementa un **cifrado simétrico tipo César**, donde:

1. Se define un mensaje secreto.
2. Se aplica una clave numérica.
3. Cada letra se transforma usando:

   * `ord()` → convierte letra a número
   * `chr()` → convierte número a letra
4. Se genera un mensaje encriptado.
5. Se solicita al usuario la clave.
6. Si la clave es correcta:

   * Se desencripta el mensaje
7. Si es incorrecta:

   * Se niega el acceso

---

## 💻 Código principal

```python
mensaje_secreto = "ESTO ES UN SECRETO"
llave_real = 5

mensaje_encriptado = ""
for letra in mensaje_secreto:
    mensaje_encriptado += chr(ord(letra) + llave_real)

print("--- SISTEMA DE SEGURIDAD ACTIVADO ---")
print(f"Mensaje encriptado recibido: {mensaje_encriptado}")

intento_llave = int(input("Ingrese la llave: "))

if intento_llave == llave_real:
    mensaje_final = ""
    for letra in mensaje_encriptado:
        mensaje_final += chr(ord(letra) - intento_llave)
    print(f"Mensaje: {mensaje_final}")
else:
    print("Acceso denegado")
```

---

## ▶️ Ejecución

Para ejecutar el programa:

```bash
python main.py
```

---

## 📊 Resultados

El sistema:

* Protege un mensaje mediante encriptación
* Solicita una clave para acceder
* Permite ver el mensaje solo si la clave es correcta

Esto demuestra cómo funciona la seguridad básica en sistemas informáticos.

---

## ⚠️ Limitaciones

* El cifrado tipo César es simple y no es seguro en la vida real
* No protege contra ataques avanzados
* Solo se usa con fines educativos

---

## 🔗 Cibergrafía

* https://www.redeszone.net/tutoriales/seguridad/criptografia-algoritmos-hash/
* https://www.cloudflare.com/es-es/learning/ssl/what-is-encryption/
* https://www.huntress.com/cybersecurity-101/topic/what-is-symmetric-encryption-algorithms

---

## 👥 Autores

* Isacc Simanca Bertel
* Laura Milena Sanchez Henao
* Alexander Loaiza Guapacha
