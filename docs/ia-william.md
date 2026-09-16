# William Prompts:

## IA utilizada: Chat Gemini

## Prompt 1:
En base a el siguiente contexto (aquí copie y pegué el enunciado de el parcial como tal).
Dime cual podría ser la mejor manera de trabajar en simultaneo y de manera remota, en un grupo de 3 personas. Tenía pensado dockerizar la BD con un docker-compose y tenerlo en un repo de github para que solo sea para los demas clonar el repo y ejecutar el docker compose.

### Respuesta a el prompt 1: 
Tu idea de usar **Docker** es excelente y, de hecho, es la forma más profesional y limpia de hacerlo. **No va a dificultar la conexión con Python ni el entregable final**.

Al exponer el puerto `3306` en Docker, para tu código en Python o DBeaver/Workbench será exactamente igual que si lo hubieras instalado de forma nativa. Para el profesor será transparente; él solo evaluará el Notebook y los PDFs.

Aquí tienes el plan de ataque óptimo para trabajar en paralelo y terminar rápido.

---

### 1. El entorno rápido (Tu idea de Docker)

Crea una carpeta compartida (vía GitHub o un .zip rápido) con dos archivos:

1. El script SQL que les dio el profesor (llámalo `init.sql`).
2. Un archivo `docker-compose.yml` con esto:

```yaml
version: '3.8'
services:
  mysql:
    image: mysql:8.0
    container_name: db_parcial
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: nombre_de_la_bd
    ports:
      - "3306:3306"
    volumes:
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql

```

Al ejecutar `docker compose up -d`, la base de datos se crea, ejecuta el script y queda lista en el puerto 3306. **Ambos deben correr esto en sus propias computadoras** para tener una copia exacta de la base de datos y trabajar sin depender de la conexión del otro.

---

### 2. División del Trabajo (Trabajo en Paralelo)

Para terminar esta noche, no pueden hacer todo juntos. Tienen que dividirse así:

vale, este es el plan que seguiremos:

## 👥 FASE 2: División del Trabajo Equilibrada (3 Personas)

Para evitar conflictos en Git, cada uno trabajará en un archivo distinto. Las Personas 2 y 3 usarán Notebooks separados temporalmente y los unirán al final. El documento de IA (Parte 5) se construirá entre todos en un Google Docs compartido desde el minuto cero.

### 🧑‍💻 Persona 1: Especialista SQL (Partes 1 y 2)

**Objetivo:** Explorar la base de datos, plantear las preguntas de negocio y resolverlas analíticamente.
  **Archivo de trabajo:** consultas_negocio.sql y el Documento PDF final de SQL.
  **Tareas:**
    1.  Conectarse a la BD en un gestor (DBeaver, VS Code, Workbench).
    2.  Definir 4 preguntas de negocio clave cruzando tablas (Ej: Ventas por cliente, rendimiento de empleados, productos más rentables).
    3.  Escribir, probar y optimizar las consultas SQL.
    4.  Crear el documento PDF con las preguntas, el código SQL y la respuesta de negocio obtenida.
    5.  Pegar en el Google Docs los prompts de IA que usó para mejorar o corregir su SQL.

### 🧑‍🔬 Persona 2: Data Scientist - Análisis Univariado (Partes 3 y 4a)
**Objetivo:** Conectar Python a la base de datos y analizar la distribución individual de los datos.
  **Archivo de trabajo:** analisis_univariado.ipynb (Archivo temporal).
  **Tareas:**
    1.  Configurar la conexión a la BD mediante mysql-connector-python o SQLAlchemy.
    2.  Cargar las tablas principales (customers, orders, products, etc.) en DataFrames de Pandas.
    3.  Generar los **10 gráficos univariados** requeridos (histogramas para variables numéricas, gráficos de barras para categóricas).
    4.  Escribir una breve interpretación debajo de cada gráfico.
    5.  Pegar en el Google Docs los prompts de IA usados para generar gráficos o corregir código.

### 🕵️ Persona 3: Data Scientist - Análisis Bivariado y Ensamblaje (Partes 4b, 5 y Entregables)
**Objetivo:** Descubrir relaciones entre variables, realizar las conclusiones finales y unificar el proyecto.
  **Archivo de trabajo:** analisis_bivariado.ipynb (Archivo temporal) -> Luego se une a analisis_parcial.ipynb.
  **Tareas:**
    1.  Copiar la misma celda de conexión a la BD y carga de DataFrames que usó la Persona 2.
    2.  Generar los **4 análisis bivariados** requeridos usando Seaborn (ej. Scatter plots cruzando Precio vs Cantidad, o Boxplots de Ventas por Categoría).
    3.  Escribir las interpretaciones detalladas de esas relaciones.
    4.  **Ensamblaje Final:** Cuando la Persona 2 termine, la Persona 3 copiará las celdas de la Persona 2 y las pegará en un archivo final llamado analisis_parcial_final.ipynb.
    5.  Darle formato al Documento de IA (Parte 5) tomando lo que los tres pegaron en el Google Docs y empaquetar la entrega final.

---

### 3. La herramienta clave: VS Code Live Share

Si en algún momento necesitan ver el código del otro, instalen la extensión **Live Share** en Visual Studio Code.
Esto les permite:

* Editar el mismo Jupyter Notebook en tiempo real (como Google Docs).
* Compartir terminales.
* Persona B puede ayudar a Persona A con el SQL, o Persona A puede sugerirle a Persona B qué variables cruzar en los gráficos bivariados de Seaborn.

---


## Validacion/limitaciones del prompt 1:

Ya teníamos en mente lo que queríamos hacer pero la IA ayudó a direccionar de una manera más explicita lo que debíamos hacer y el como, montamos el repo, con un readme para explicar como montar el docker y como trabajar en el, se montó tambien el script SQL que el profe mandó para apartir de ahí generar la BD dentro de el Docker. Esto nos permitió trabajar de manera remota y asíncrona en el mismo trabajo, ya que la IA también nos ayudó a repartir responsabilidades de una manera organizada y de forma que no chocaramos.