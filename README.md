#🔐 **Encriptación y Seguridad Informática**

##📄 Descripción

Este proyecto tiene como objetivo explicar la importancia de la seguridad informática mediante la implementación de técnicas básicas de protección de datos.

Se desarrollan dos enfoques principales:

Cifrado tipo César para comprender la lógica de la encriptación.
Uso de hashing con bcrypt y base de datos SQLite para simular un sistema real de autenticación.

##📊 Dataset

No se utiliza un dataset externo.

Los datos son generados dentro del sistema, específicamente usuarios y contraseñas almacenadas en una base de datos SQLite (seguridad.db).

🛠 Tecnologías
Python
bcrypt
sqlite3
pandas

##⚙️ Implementación

El proyecto se divide en dos partes:

🔐 1. Cifrado César (Simétrico)
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
🗄️ 2. Base de datos (SQLite)
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
👤 3. Registro de usuarios (bcrypt)
import bcrypt

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
🔑 4. Validación de login
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
🧪 5. Prueba del sistema
registrar_usuario("analista_juan", "MiClaveSegura123")
registrar_usuario("laura", "1234567890")
registrar_usuario("alex", "1234567890")

usuario = input("Usuario: ")
password = input("Contraseña: ")

validar_login(usuario, password)

##▶️ Ejecución

Instalar dependencias:

pip install bcrypt pandas

Ejecutar el programa:

python main.py
📈 Resultados

El sistema permite:

Encriptar y desencriptar mensajes.
Registrar usuarios en una base de datos.
Proteger contraseñas mediante hashing seguro.
Validar el acceso correctamente.

##👥 Autores

###Isacc Simanca Bertel

###Laura Milena Sanchez Henao

###Alexander Loaiza Guapacha
