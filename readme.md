# 🏆 World Cup Database (Bash ETL & PostgreSQL Analytics)

Proyecto interactivo de automatización y análisis de datos sobre mundiales de fútbol. Incluye la creación de la base de datos relacional, un script de Bash para procesamiento e inserción masiva desde un CSV, y una suite de consultas analíticas avanzadas.

---

## ⚡ Flujo de Automatización (ETL)

```mermaid
flowchart LR
    A[games.csv] -->|Lectura & Parsing| B[insert_data.sh]
    B -->|Comprobación de Duplicados| C[(PostgreSQL)]
    C -->|Consultas Analíticas| D[queries.sh]
```

## ✨ Características y Conceptos Clave
* **Scripting Bash para Carga de Datos `(insert_data.sh)`:**
  * Lectura automatizada de archivos CSV delimitados por comas.
  * Lógica condicional para evitar duplicados de equipos (`teams`) antes de insertar los partidos (`games`).
  * Ejecución de comandos PostgreSQL vía `psql` desde la terminal de Bash.
* **Modelado Relacional Relacionado:**
  * Uso de claves primarias (`PRIMARY KEY`), foráneas (`FOREIGN KEY`) y restricciones de unicidad (`UNIQUE`).
* **Análisis de Datos con SQL Avanzado (`queries.sh`):**
  * Agregaciones complejas (`AVG`, `SUM`, `COUNT`, `ROUND`).
  * Consultas relacionales con múltiples `JOIN` entre tablas de equipos y partidos.
  * Agrupamientos y filtros avanzados (`GROUP BY`, `ORDER BY`, `LIKE`).
 
## 🛠️ Tecnologías Utilizadas
* **Base de Datos:** PostgreSQL
* **Lenguaje de Scripting:** Bash / Shell Scripting
* **Fuente de Datos:** CSV (Comma-Separated Values)

## 🚀 Cómo Ejecutar el Proyecto
### Prerrequisitos
Tener instalado PostgreSQL y la herramienta de línea de comandos `psql`.
### Pasos de Configuración
1. **Clonar el repositorio:**
   ```bash
      git clone https://github.com/Aki-new/world-cup-database.git
      cd world-cup-database
   ```
2. **Crear e importar la base de datos base:**
   ```bash
      psql -U postgres < worldcup.sql
   ```
3. **Dar permisos de ejecución a los scripts:**
   ```bash
      chmod +x insert_data.sh queries.sh
   ```
4. **Poblar la base de datos desde el CSV:**
   ```bash
      ./insert_data.sh
   ```
5. **Ejecutar el reporte de consultas SQL:**
   ```bash
      ./queries.sh
   ```

## 📊 Ejemplos de Consultas Analíticas (Queries)
```SQL
   -- Promedio de goles marcados por equipos ganadores redondeado a 2 decimales
   SELECT ROUND(AVG(winner_goals), 2) FROM games;

   -- Equipos que han ganado la copa (orden alfabético)
   SELECT DISTINCT(name) 
   FROM teams 
   INNER JOIN games ON teams.team_id = games.winner_id 
   WHERE round = 'Final' 
   ORDER BY name;
```

---

## 📜 Créditos y Reconocimientos

* **Origen de la consigna / dataset:** Este proyecto es uno de los desafíos requeridos para la obtención de la **Certificación de Bases de Datos Relacionales** de [freeCodeCamp](https://www.freecodecamp.org/).
* **Implementación:** La lógica de scripts en Bash (`insert_data.sh`), la estructuración del esquema PostgreSQL (`worldcup.sql`) y la elaboración de consultas analíticas (`queries.sh`) fueron desarrolladas por completo como resolución individual al problema planteado.
