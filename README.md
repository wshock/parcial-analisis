# 🚀 Estrategia de Trabajo en Equipo - Parcial de Datos (ClassicModels)

Este documento define el flujo de trabajo, la configuración del entorno y la división de tareas para que los 3 integrantes del equipo trabajen en paralelo. Todos tendrán un rol de desarrollo activo (SQL o Python) y la carga estará equilibrada.

---

## 🛠️ FASE 1: Configuración del Entorno (Cada integrante debe hacer esto)

Para que todos trabajen con la misma versión de la base de datos y de las librerías, todos deben seguir estos pasos en sus computadoras:

### 1. Clonar el repositorio y Levantar Docker
Abre tu terminal, clona el repositorio y levanta la base de datos local:
```bash
git clone <URL_DEL_REPOSITORIO>
cd <NOMBRE_DE_LA_CARPETA>

# Levantar BD en segundo plano (Requiere Docker Desktop abierto)
docker compose up -d
```

### 2. Configurar Python y el Entorno Virtual
En la misma terminal, crea y activa tu entorno virtual:
```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual (Windows)
.\venv\Scripts\activate
# Activar entorno virtual (Mac/Linux)
source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt
```

## 📦 Lista de Verificación (Checklist Final 11:59 pm)
- [ ] **Entregable 1:** Documento PDF con las 4 preguntas de negocio y sus consultas SQL (Persona 1).
- [ ] **Entregable 2:** Notebook `analisis_parcial_final.ipynb` unificado (Conexión + 10 univariados + 4 bivariados + Conclusiones). Subido a la plataforma o a Drive (Personas 2 y 3).
- [ ] **Entregable 3:** Documento sobre el uso de la IA y buenas prácticas (Todos aportan, Persona 3 consolida).
Estrategia_Equipo_Equilibrada.md
Mostrando Estrategia_Equipo_Equilibrada.md.