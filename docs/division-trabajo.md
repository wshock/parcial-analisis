# FASE 2: División del Trabajo Equilibrada (3 Personas)

Para evitar conflictos en Git, cada uno trabajará en un archivo distinto. Las Personas 2 y 3 usarán Notebooks separados temporalmente y los unirán al final. El documento de IA (Parte 5) se construirá entre todos en un Google Docs compartido desde el minuto cero.

---

## Persona 1: Especialista SQL (Partes 1 y 2)

**Objetivo:** Explorar la base de datos, plantear las preguntas de negocio y resolverlas analíticamente.

**Archivo de trabajo:** `consultas_negocio.sql` y el Documento PDF final de SQL.

**Tareas:**

1. Conectarse a la BD en un gestor (DBeaver, VS Code, Workbench).
2. Definir 4 preguntas de negocio clave cruzando tablas (Ej: Ventas por cliente, rendimiento de empleados, productos más rentables).
3. Escribir, probar y optimizar las consultas SQL.
4. Crear el documento PDF con las preguntas, el código SQL y la respuesta de negocio obtenida.
5. Pegar en el Google Docs los prompts de IA que usó para mejorar o corregir su SQL.

---

## Persona 2: Data Scientist - Análisis Univariado (Partes 3 y 4a)

**Objetivo:** Conectar Python a la base de datos y analizar la distribución individual de los datos.

**Archivo de trabajo:** `analisis_univariado.ipynb` (archivo temporal).

**Tareas:**

1. Configurar la conexión a la BD mediante mysql-connector-python o SQLAlchemy.
2. Cargar las tablas principales (customers, orders, products, etc.) en DataFrames de Pandas.
3. Generar los **10 gráficos univariados** requeridos (histogramas para variables numéricas, gráficos de barras para categóricas).
4. Escribir una breve interpretación debajo de cada gráfico.
5. Pegar en el Google Docs los prompts de IA usados para generar gráficos o corregir código.

---

## Persona 3: Data Scientist - Análisis Bivariado y Ensamblaje (Partes 4b, 5 y Entregables)

> **Asignada a:** Hanner (tú)

**Objetivo:** Descubrir relaciones entre variables, realizar las conclusiones finales y unificar el proyecto.

**Archivo de trabajo:** `analisis_bivariado.ipynb` (archivo temporal) → Luego se une a `analisis_parcial.ipynb`.

**Tareas:**

1. Copiar la misma celda de conexión a la BD y carga de DataFrames que usó la Persona 2.
2. Generar los **4 análisis bivariados** requeridos usando Seaborn (ej. Scatter plots cruzando Precio vs Cantidad, o Boxplots de Ventas por Categoría).
3. Escribir las interpretaciones detalladas de esas relaciones.
4. **Ensamblaje final:** Cuando la Persona 2 termine, copiar las celdas de la Persona 2 y pegarlas en un archivo final llamado `analisis_parcial_final.ipynb`.
5. Darle formato al Documento de IA (Parte 5) tomando lo que los tres pegaron en el Google Docs y empaquetar la entrega final.
