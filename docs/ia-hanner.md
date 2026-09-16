# Hanner

a la ia se le subió el contexto de todo el enunciado y la división que habíamos hecho del trabajo, esto por medio de archivos markdown.

Se escribía un prompt y luego se le pasaba a chatgpt para que mejorara el prompt para ahí sí pasarloa al agente que estaba conectado al proyecto

ejemplo:
Prompt: dime la mejor forma de explorar todas las tablas para yo mismo llegar a una conclusión de encontrar relaciones entre variables

Prompt mejorado:
Quiero explorar de manera sistemática todas las tablas de mi base de datos para identificar por mí mismo posibles relaciones entre variables y encontrar oportunidades para realizar análisis univariados y bivariados.

No quiero que me des directamente las conclusiones ni que elijas por mí las relaciones más importantes. Quiero que me guíes paso a paso para descubrirlas.

Para cada tabla, ayúdame a:

1. Entender cuál es su propósito dentro del modelo.
2. Identificar sus columnas, tipos de datos y claves primarias/foráneas.
3. Conocer la cantidad de registros y revisar algunos ejemplos de datos.
4. Identificar variables categóricas, numéricas y temporales que puedan ser interesantes.
5. Analizar valores nulos, valores únicos, rangos y posibles valores atípicos cuando sea relevante.
6. Entender con qué otras tablas se puede relacionar y mediante qué claves.
7. Proponer consultas exploratorias de SQL que me permitan investigar los datos.

Después de explorar cada tabla, hazme preguntas orientadoras como: "¿qué observas?", "¿qué variable podría estar relacionada con esta otra?" o "¿qué hipótesis podrías plantear?". Deja que yo interprete los resultados antes de darme tu opinión.

Cuando terminemos la exploración, ayúdame a convertir mis propias observaciones en posibles preguntas de negocio y análisis bivariados.

La base de datos es MySQL y corresponde a ClassicModels. Las tablas son:

* customers
* employees
* offices
* orderdetails
* orders
* payments
* productlines
* products

Quiero priorizar la comprensión del modelo y de los datos sobre generar muchas consultas. Explícame cada paso de forma sencilla y dame solo el siguiente paso cuando te confirme que estoy listo para continuar.


prompt:quiero agrupar una tabla por los valores categóricos de una columna y que me diga cuántos hay de cada uno, qué consulta debería hacer en python

promp: quiero ver la cantidad de customers que tiene cada empleado, para eso primero necesito hacer un join y luego agrupar con empleado, verdad? si es así, cómo haría eso en python?

----
Consultapara ver todas las columnas
SELECT 
	table_name AS tabla,
    table_rows AS registros
FROM information_schema.tables
WHERE table_schema = 'classicmodels'
AND table_type = 'BASE TABLE'
ORDER BY table_name;


Explícame qué es un análisis bivariado