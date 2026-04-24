# 🔐 **Encriptación y Seguridad Informática**

## 📄 Descripción

Este proyecto tiene como objetivo explicar la importancia de la seguridad informática y la encriptación en la protección de la información. Hoy en día, los datos son un recurso valioso, por lo que es fundamental evitar accesos no autorizados.

Se presentan conceptos clave como el cifrado simétrico, asimétrico y las funciones hash, así como las principales áreas de la seguridad informática: hardware, software y red.

En la parte práctica, se implementa un cifrado César para comprender el funcionamiento básico de la encriptación y un sistema más avanzado de autenticación que utiliza bcrypt y SQLite, demostrando cómo se protegen las contraseñas en aplicaciones reales.

## 📊 Dataset

No se utiliza un dataset externo.

Los datos son generados dentro del sistema, específicamente usuarios y contraseñas almacenadas en una base de datos SQLite (seguridad.db).


## 🛠 Tecnologías

- [Python](https://www.python.org/)
- [bcrypt](https://pypi.org/project/bcrypt/)
- [sqlite3](https://docs.python.org/3/library/sqlite3.html)
- [pandas](https://pandas.pydata.org/)

## ⚙️ Implementación

El proyecto se divide en dos partes principales:

---

### 🔐 1. Cifrado César (Simétrico)

```python
mensaje_secreto = "ESTO ES UN SECRETO"
llave_real = 5

mensaje_encriptado = ""
for letra in mensaje_secreto:
    mensaje_encriptado += chr(ord(letra) + llave_real)

print("--- SISTEMA DE SEGURIDAD ACTIVADO ---")
print(f"Mensaje encriptado recibido: {mensaje_encriptado}")
print("-------------------------------------")

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

### 🗄️ 2. Base de Datos (SQLite)

```python
import sqlite3

conexion = sqlite3.connect('seguridad.db')
cursor = conexion.cursor()

cursor.execute('DROP TABLE IF EXISTS Usuarios')

cursor.execute('''
    CREATE TABLE Usuarios (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nombre TEXT NOT NULL,
        password_hash BLOB NOT NULL
    )
''')

conexion.commit()
conexion.close()
```

---

### 👤 3. Registro de Usuarios (bcrypt)

```python
import bcrypt
import sqlite3

def registrar_usuario(nombre_usuario, clave_plana):
    sal = bcrypt.gensalt()
    hash_encriptado = bcrypt.hashpw(clave_plana.encode('utf-8'), sal)

    conexion = sqlite3.connect('seguridad.db')
    cursor = conexion.cursor()

    try:
        cursor.execute(
            "INSERT INTO Usuarios (nombre, password_hash) VALUES (?, ?)",
            (nombre_usuario, hash_encriptado)
        )
        conexion.commit()
        print(f"Usuario '{nombre_usuario}' registrado con éxito.")

    except Exception as e:
        print(f"Error: {e}")

    finally:
        conexion.close()
```

---

### 🔑 4. Validación de Login

```python
import sqlite3
import bcrypt

def validar_login(nombre_usuario, clave_intento):
    conexion = sqlite3.connect('seguridad.db')
    cursor = conexion.cursor()

    cursor.execute(
        "SELECT password_hash FROM Usuarios WHERE nombre = ?",
        (nombre_usuario,)
    )

    resultado = cursor.fetchone()
    conexion.close()

    if resultado:
        hash_guardado = resultado[0]

        if bcrypt.checkpw(clave_intento.encode('utf-8'), hash_guardado):
            print(f"Acceso concedido. Bienvenido, {nombre_usuario}.")
        else:
            print("Contraseña incorrecta.")
    else:
        print("El usuario no existe.")
```

---

### 🧪 5. Prueba del Sistema

```python
registrar_usuario("analista_juan", "MiClaveSegura123")
registrar_usuario("laura", "1234567890")
registrar_usuario("alex", "1234567890")

usuario = input("Usuario: ")
password = input("Contraseña: ")

validar_login(usuario, password)
```

## ▶️ Ejecución

Para ejecutar el proyecto, sigue estos pasos:

### 📦 1. Instalar dependencias

```bash
pip install bcrypt pandas
```

---

### ▶️ 2. Ejecutar el programa

```bash
python main.py
```

---

## 📈 Resultados

El sistema desarrollado permite:

- 🔐 Encriptar y desencriptar mensajes mediante el cifrado César.
- 👤 Registrar usuarios en una base de datos SQLite.
- 🔒 Proteger contraseñas utilizando hashing seguro con bcrypt.
- ✅ Validar el acceso de usuarios de forma segura.

Además, se evidencia la diferencia entre un método de cifrado básico y técnicas modernas utilizadas en sistemas reales de seguridad informática.

## 👥 Autores

* **Isacc Simanca Bertel**

* **Laura Milena Sanchez Henao**

* **Alexander Loaiza Guapacha**
