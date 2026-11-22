# ­ƒÅå World Cup Database (Bash ETL & PostgreSQL Analytics)

*­ƒç║­ƒç© [Read this in English](README.md)*

Proyecto interactivo de automatizaci├│n y an├ílisis de datos sobre mundiales de f├║tbol. Incluye la creaci├│n de la base de datos relacional, un script de Bash para procesamiento e inserci├│n masiva desde un CSV, y una suite de consultas anal├¡ticas avanzadas.

---

## ÔÜí Flujo de Automatizaci├│n (ETL)

```mermaid
flowchart LR
    A[games.csv] -->|Lectura & Parsing| B[insert_data.sh]
    B -->|Comprobaci├│n de Duplicados| C[(PostgreSQL)]
    C -->|Consultas Anal├¡ticas| D[queries.sh]
```

## Ô£¿ Caracter├¡sticas y Conceptos Clave
* **Scripting Bash para Carga de Datos `(insert_data.sh)`:**
  * Lectura automatizada de archivos CSV delimitados por comas.
  * L├│gica condicional para evitar duplicados de equipos (`teams`) antes de insertar los partidos (`games`).
  * Ejecuci├│n de comandos PostgreSQL v├¡a `psql` desde la terminal de Bash.
* **Modelado Relacional Relacionado:**
  * Uso de claves primarias (`PRIMARY KEY`), for├íneas (`FOREIGN KEY`) y restricciones de unicidad (`UNIQUE`).
* **An├ílisis de Datos con SQL Avanzado (`queries.sh`):**
  * Agregaciones complejas (`AVG`, `SUM`, `COUNT`, `ROUND`).
  * Consultas relacionales con m├║ltiples `JOIN` entre tablas de equipos y partidos.
  * Agrupamientos y filtros avanzados (`GROUP BY`, `ORDER BY`, `LIKE`).
 
## ­ƒøá´©Å Tecnolog├¡as Utilizadas
* **Base de Datos:** PostgreSQL
* **Lenguaje de Scripting:** Bash / Shell Scripting
* **Fuente de Datos:** CSV (Comma-Separated Values)

## ­ƒÜÇ C├│mo Ejecutar el Proyecto
### Prerrequisitos
Tener instalado PostgreSQL y la herramienta de l├¡nea de comandos `psql`.
### Pasos de Configuraci├│n
1. **Clonar el repositorio:**
   ```bash
      git clone https://github.com/Akisolu/world-cup-database.git
      cd world-cup-database
   ```
2. **Crear e importar la base de datos base:**
   ```bash
      psql -U postgres < worldcup.sql
   ```
3. **Dar permisos de ejecuci├│n a los scripts:**
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

## ­ƒôè Ejemplos de Consultas Anal├¡ticas (Queries)
```SQL
   -- Promedio de goles marcados por equipos ganadores redondeado a 2 decimales
   SELECT ROUND(AVG(winner_goals), 2) FROM games;

   -- Equipos que han ganado la copa (orden alfab├®tico)
   SELECT DISTINCT(name) 
   FROM teams 
   INNER JOIN games ON teams.team_id = games.winner_id 
   WHERE round = 'Final' 
   ORDER BY name;
```

---

## ­ƒô£ Cr├®ditos y Reconocimientos

* **Origen de la consigna / dataset:** Este proyecto es uno de los desaf├¡os requeridos para la obtenci├│n de la **Certificaci├│n de Bases de Datos Relacionales** de [freeCodeCamp](https://www.freecodecamp.org/).
* **Implementaci├│n:** La l├│gica de scripts en Bash (`insert_data.sh`), la estructuraci├│n del esquema PostgreSQL (`worldcup.sql`) y la elaboraci├│n de consultas anal├¡ticas (`queries.sh`) fueron desarrolladas por completo como resoluci├│n individual al problema planteado.
