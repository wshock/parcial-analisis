# Uso de inteligencia artificial y buenas prácticas

**Proyecto:** Parcial — Análisis de datos (ClassicModels)  
**Equipo:** Hanner, William, Juanpa  
**Documento:** Entregable Parte 5 (uso de IA)

---

## 1. Herramientas de IA utilizadas

| Integrante | Herramienta(s) | Rol en el equipo |
|------------|----------------|------------------|
| William | Chat Gemini | Organización del trabajo, Docker/GitHub, división de tareas |
| Juanpa | Claude (Anthropic), chat web | Conexión BD, notebook, 10 gráficos univariados |
| Hanner | ChatGPT (mejora de prompts) + agente de Cursor conectado al proyecto | Exploración del modelo, análisis bivariado, ensamblaje del notebook y este documento |

La IA se usó como **apoyo** para investigar, comprender conceptos, construir código/consultas e interpretar resultados. El análisis, la validación con datos reales y las conclusiones finales son responsabilidad del equipo.

---

## 2. Actividades en las que fueron utilizadas

### William
- Definir cómo trabajar en paralelo de forma remota (3 personas).
- Diseñar el entorno con Docker (`docker-compose`) + repositorio GitHub.
- Proponer y afinar la **división equilibrada del trabajo** (Persona 1 SQL, Persona 2 univariado, Persona 3 bivariado/ensamblaje).

### Juanpa
- Levantar la BD con Docker y verificar que `init.sql` cargó `classicmodels` (8 tablas).
- Conectar Python a MySQL desde el notebook (`mysql-connector-python`).
- Elegir 10 columnas según tipo de dato y generar los gráficos univariados con interpretación.

### Hanner
- Cargar contexto del enunciado y de la división del trabajo (archivos Markdown).
- Mejorar prompts en ChatGPT antes de pasarlos al agente del proyecto.
- Explorar tablas de forma guiada (sin que la IA eligiera las conclusiones).
- Aprender joins/agrupaciones en pandas, concepto de análisis bivariado.
- Formalizar las 4 preguntas bivariadas, gráficos, limpieza de atípicos e interpretaciones.
- Unificar notebooks y consolidar este documento de IA.

---

## 3. Principales prompts o instrucciones empleados

### William — Plan de trabajo y Docker

**Prompt (resumen):**  
Con el enunciado del parcial como contexto: ¿cuál es la mejor manera de trabajar en simultáneo y de forma remota en un grupo de 3? Idea previa: dockerizar la BD con `docker-compose` y un repo en GitHub para que los demás solo clonen y ejecuten Compose.

**Uso del resultado:** Se montó el repo, el `README`, el `docker-compose.yml` y el `init.sql`, y se adoptó la división por archivos para evitar conflictos en Git.

---

### Juanpa — BD, conexión y univariado

- *«La base de datos corre en un contenedor de Docker definido en docker-compose.yml. ¿Cómo verifico que el script init.sql creó la base classicmodels con sus 8 tablas antes de conectarme desde Python?»*
- *(Con captura del gráfico y estadísticas)* *«Revisa este gráfico y sus estadísticas para confirmar que el resultado es correcto antes de escribir la interpretación.»*
- *«Antes de subir el notebook al repositorio, ¿cómo compruebo que se ejecuta completo de arriba a abajo y que solo voy a subir mi archivo?»*

---

### Hanner — Exploración, bivariado e interpretación

**Flujo:** se escribía un prompt → ChatGPT lo mejoraba → se enviaba al agente conectado al proyecto.

**Prompt inicial (ejemplo):**  
*«Dime la mejor forma de explorar todas las tablas para yo mismo llegar a una conclusión de encontrar relaciones entre variables.»*

**Prompt mejorado (usado con el agente):** exploración sistemática tabla por tabla (propósito, columnas, claves, nulos, relaciones), sin que la IA entregue las conclusiones; guía paso a paso; preguntas orientadoras; ClassicModels; priorizar comprensión sobre muchas consultas.

**Otros prompts:**
- Agrupar por valores categóricos y contar en Python (`value_counts` / `groupby`).
- Join + agrupar para cantidad de customers por empleado.
- *«Explícame qué es un análisis bivariado.»*
- Tras explorar: *«¿Cuál de estas curiosidades refleja un análisis bivariado?»* (listado de hipótesis por tabla).
- Formalizar las 4 preguntas bivariadas y el método (pregunta → variables → gráfico → interpretación).
- *«¿Qué opinas de esta conclusión?»* (revisión de interpretaciones propias, no reemplazo del análisis).

**Las 4 preguntas bivariadas elegidas por el estudiante:**
1. Tiempo `orderDate`→`shippedDate` vs país del cliente.
2. Monto del pedido vs tiempo de envío.
3. País del cliente vs `creditLimit`.
4. `quantityInStock` vs cantidad vendida histórica del producto.

---

## 4. Forma en que validaron los resultados

| Qué se validó | Cómo |
|---------------|------|
| BD instalada | `SHOW DATABASES` / `SHOW TABLES` desde Docker; 8 tablas de ClassicModels |
| Conexión Python | Celda de prueba de imports; carga de tablas y `.shape` (ej. customers: 122 filas) |
| Notebook completo | *Restart Kernel + Run All* de arriba a abajo |
| Gráficos univariados | Comparar con estadísticas reales (`describe`, conteos) antes de interpretar |
| Gráficos bivariados | Ejecutar merges/cálculos en pandas; revisar medianas, correlaciones y atípicos en los datos |
| SQL / código sugerido por IA | Probarlo contra la BD o DataFrames reales; no aceptar resultados sin ejecutarlos |
| Interpretaciones | El estudiante escribe la conclusión; la IA solo comenta o sugiere matices |
| Git | `git status` / `git pull` antes de subir para no pisar trabajo del equipo |

---

## 5. Errores o limitaciones encontrados

1. **Puerto 3306 ocupado / Access denied:** en un entorno el contenedor usó `3307` y la conexión por defecto al 3306 fallaba con credenciales distintas. Había que alinear puerto del Compose con el del notebook.
2. **Columnas DECIMAL como `object`:** `mysql-connector` trae `Decimal`; `describe()` no daba bien promedio/mínimo. Solución: convertir a `float` tras cargar.
3. **País duplicado (“Norway”):** espacios al final → 28 países en vez de 27. Solución: `str.strip()` en columnas de texto.
4. **Atípico extremo (Singapore, ~60 días de envío):** distorsionaba el boxplot de días de envío; se documentó limpieza IQR solo en Singapore.
5. **Instrucciones desactualizadas de la IA:** botones/páginas que ya no existen; hubo que corregir con capturas.
6. **Kernel reiniciado:** al reabrir VS Code se pierden variables; hay que reejecutar desde el inicio.
7. **Sangría al pegar código:** errores de indentación al copiar desde el chat.
8. **La IA no ve la pantalla ni los datos reales:** depende de lo que el estudiante pegue o ejecute; puede alucinar o generalizar.
9. **Divergencia en Git (`pull`):** ramas divergentes; hubo que usar `git pull --rebase` de forma explícita.
10. **Nombres de DataFrames distintos** entre notebooks (`customers` vs `df_customers`): al unificar el notebook final se alinearon nombres para que una sola conexión baste.

---

## 6. Buenas prácticas aplicadas

- **No copiar sin comprender:** se pidió explicación de comandos y de cada paso; las interpretaciones de gráficos las escribió el equipo.
- **Probar siempre:** consultas, celdas y notebooks se ejecutaron contra la BD/DataFrames reales.
- **Verificar resultados:** `.shape`, `describe`, conteos, correlación y revisión visual de gráficos antes de concluir.
- **Interpretar con criterio propio:** la IA orientaba; el estudiante decidía hipótesis, preguntas bivariadas y redacción final.
- **Proteger credenciales:** uso de `getpass` para la contraseña; no dejar secretos en claro en el repo.
- **Entorno limpio:** `venv` e inclusión en `.gitignore`.
- **Trabajo en equipo seguro:** archivos separados por persona, `git pull` antes de push, un solo notebook final consolidado.
- **Responsabilidad del contenido:** el equipo asume lo entregado (código, gráficos, conclusiones y este documento), aunque la IA haya apoyado en el proceso.

---
