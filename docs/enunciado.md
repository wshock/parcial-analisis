# ENUNCIADO PARCIAL

El objetivo del parcial es evaluar sus habilidades en el análisis de datos desde SQL y Python. Por eso, debes seguir los siguientes pasos completando cada uno de ellos de forma organizada. Pueden realizarlo en equipos de **MÁXIMO 3 PERSONAS**.

---

## Parte 1: Instalación de la BD enviada

Adjunto se encuentran los archivos SQL de la BD a trabajar. Debes instalarla de forma local en un motor **MySQL**. Asegúrate de instalar todo en una nueva BD con el comando:

```sql
CREATE DATABASE nombre_de_la_bd;
```

Luego de instalar la BD, explora su contenido, tabla por tabla, identificando su propósito, cantidades de datos y tablas principales.

---

## Parte 2: Resolución de preguntas de negocio

Después de instalar y conocer mejor la BD enviada, identifica y responde **cuatro preguntas de negocio clave** siguiendo la plantilla trabajada en clase, con los pasos y apartados que esta contiene.

---

## Parte 3: Conexión a la BD desde Visual Studio Code

Usando VSC vas a instalar la extensión **Jupyter** para poder trabajar con notebooks desde este ambiente. Luego, deben conectarse a la base de datos instalada usando alguna librería que tenga este propósito. Tres que pueden servir son:

- **MySQL Connector/Python** → `pip install mysql-connector-python`
- **PyMySQL** → `pip install pymysql`
- **SQLAlchemy** → `pip install sqlalchemy`

Normalmente estas librerías usan un objeto conexión que contiene usuario, contraseña y nombre de la BD y, a través de este objeto se abre un cursor desde el cual llamar un método `execute` donde se envían queries que son ejecutados en la BD y retornan los datos hacia un dataframe de pandas. Les comparto un pequeño código pero parte del ejercicio es que investiguen cómo realizar esta parte por su cuenta.

```python
import mysql.connector

# Establecer la conexión
try:
    connection = mysql.connector.connect(
        host='localhost',        # Cambia esto por tu host
        user='tu_usuario',       # Cambia esto por tu usuario
        password='tu_contraseña', # Cambia esto por tu contraseña
        database='nombre_bd'     # Cambia esto por el nombre de tu base de datos
    )

    if connection.is_connected():
        print("Conexión exitosa a la base de datos")

        # Crear un cursor
        cursor = connection.cursor()

        # Ejecutar una consulta
        cursor.execute("SELECT * FROM nombre_tabla")  # Cambia esto por tu nombre de tabla

        # Recuperar los resultados
        resultados = cursor.fetchall()
        for fila in resultados:
            print(fila)

except mysql.connector.Error as err:
    print(f"Error: {err}")

finally:
    # Cerrar la conexión y el cursor
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("Conexión cerrada")
```

---

## Parte 4: Análisis exploratorio del modelo desde Python

Usando **matplotlib** o **seaborn** realicen un análisis exploratorio del modelo. Por lo menos deben explorar **10 columnas** según su tipo de dato y mostrar un gráfico con sus datos, y **4 análisis bivariados**, es decir, analizar dos columnas que puedan tener relación e interpretar dicha relación.

---

## Parte 5: Ayuda utilizando modelos LLM

Durante el desarrollo del parcial podrán utilizar herramientas de inteligencia artificial como apoyo para investigar, comprender conceptos, construir consultas SQL, revisar código e interpretar resultados. La IA no debe reemplazar el análisis del estudiante. Todo código, consulta, gráfico y conclusión generada debe ser revisado, probado y validado con los datos reales de la base de datos.

Deberán entregar un documento adicional en formato PDF o Word que incluya:

- Herramientas de IA utilizadas.
- Actividades en las que fueron utilizadas.
- Principales prompts o instrucciones empleados.
- Forma en que validaron los resultados.
- Errores o limitaciones encontrados.
- Buenas prácticas aplicadas.

Entre las buenas prácticas se deben considerar: no copiar respuestas sin comprenderlas, probar las consultas SQL, verificar los resultados, interpretar los gráficos con criterio propio, proteger contraseñas y datos sensibles, y asumir la responsabilidad por el contenido final entregado.

---

## Entregables

Se habilitará una tarea en Unac virtual para subir los siguientes archivos:

1. Documento o PDF con las 4 preguntas elegidas y resueltas por medio de consultas SQL.
2. Notebook con la conexión a la BD, el análisis univariado y bivariado y las conclusiones y recomendaciones. Si el notebook es muy pesado para subirlo a Unac virtual, subirlo a Drive y compartir el enlace.
3. Documento sobre el uso de la IA y las buenas prácticas aplicadas.

---

**Fecha de entrega:** Miércoles 16 de septiembre 2026, 11:59 pm
