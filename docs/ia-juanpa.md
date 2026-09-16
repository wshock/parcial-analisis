# Juanpa


## Herramienta usada
Claude (Anthropic), en el chat web. Le pasé el enunciado, el diagrama de la base de datos, el README del repo y la división del trabajo, y le pedí que me guiara paso a paso, explicando el porqué de cada paso.

## Actividades en las que la usé
- Levantar la base de datos con Docker y comprobar que cargó bien.
- Conectar Python con MySQL desde el notebook.
- Elegir las 10 columnas según su tipo de dato y generar los gráficos univariados.

## Principales prompts
Prompt: "La base de datos corre en un contenedor de Docker definido en docker-compose.yml. ¿Cómo verifico que el script init.sql creó la base classicmodels con sus 8 tablas antes de conectarme desde Python?"

Prompt: (con captura del gráfico y los resultados) "Revisa este gráfico y sus estadísticas para confirmar que el resultado es correcto antes de escribir la interpretación."

Prompt: "Antes de subir el notebook al repositorio, ¿cómo compruebo que se ejecuta completo de arriba a abajo y que solo voy a subir mi archivo?"

## Cómo validé los resultados
- Comprobé que la base cargó con SHOW DATABASES y SHOW TABLES desde Docker (aparecieron las 8 tablas).
- Probé el notebook con una celda que solo importa las librerías antes de conectar.
- Revisé el tamaño de cada tabla con .shape (por ejemplo, customers con 122 filas).
- Al final reinicié el kernel y ejecuté todo con Restart + Run All para confirmar que el notebook corre de arriba a abajo sin errores.

## Errores y limitaciones encontrados
- **Columnas decimales leídas como texto:** creditLimit salía con dtype object y describe() no mostraba promedio ni mínimo. La causa es que mysql-connector trae los DECIMAL como tipo Decimal. Lo arreglé convirtiendo esas columnas a float justo después de cargar las tablas.
- **País duplicado:** en el gráfico de country, "Norway" aparecía dos veces porque uno tenía espacios al final. Salían 28 países en vez de 27. Lo corregí con str.strip() y lo apliqué también a las demás columnas de texto.
- **Instrucciones desactualizadas:** la IA me indicó un botón de descarga de Python que ya no existía así en la página. Tuve que mandar captura para que me corrigiera.
- **Kernel reiniciado:** al volver a abrir VS Code, el notebook olvidó los imports y hubo que ejecutar las celdas desde el inicio.
- **Sangría en Python:** al pegar código al final de una celda quedaron espacios mal puestos; fue necesario revisar la indentación.
- La IA no ve mi pantalla, así que dependía de las capturas y los resultados que yo le pegaba.

## Buenas prácticas aplicadas
- No copié los pasos sin entenderlos: pedí que me explicara qué hacía cada comando y cada línea de código.
- Protegí la contraseña con getpass, así no queda escrita en el notebook que se sube a GitHub.
- Usé un entorno virtual (venv), que está en el .gitignore para no subirlo al repo.
- Revisé con git status que solo subiera mi notebook.
- Hice git pull antes de subir para no pisar el trabajo de mis compañeros.
- Revisé cada gráfico con los números reales antes de escribir la interpretación, y asumo la responsabilidad del contenido entregado.