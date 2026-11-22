# 🏆 World Cup Database (Bash ETL & PostgreSQL Analytics)

**What it does:** Loads historical World Cup data from a CSV file into a database and answers questions such as average goals or which teams won finals.  
**Why it matters:** Data scattered in a CSV makes statistical questions slow and unreliable to answer.

**Qué hace:** Carga datos históricos de mundiales desde un archivo CSV a una base de datos y responde preguntas como el promedio de goles o qué equipos ganaron finales.  
**Por qué importa:** Los datos dispersos en un CSV hacen lentas y poco confiables las preguntas estadísticas.

> 📄 Versión completa en español: [README.es.md](README.es.md)

Interactive automation and data analysis project about football world cups. It includes the creation of the relational database, a Bash script for mass processing and insertion from a CSV, and a suite of advanced analytical queries.

---

## ⚡ Automation Flow (ETL)

```mermaid
flowchart LR
    A[games.csv] -->|Reading & Parsing| B[insert_data.sh]
    B -->|Duplicate Checking| C[(PostgreSQL)]
    C -->|Analytical Queries| D[queries.sh]
```

## ✨ Key Features and Concepts
* **Bash Scripting for Data Loading `(insert_data.sh)`:**
  * Automated reading of comma-delimited CSV files.
  * Conditional logic to avoid duplicate teams (`teams`) before inserting matches (`games`).
  * Execution of PostgreSQL commands via `psql` from the Bash terminal.
* **Relational Data Modeling:**
  * Use of primary keys (`PRIMARY KEY`), foreign keys (`FOREIGN KEY`), and unique constraints (`UNIQUE`).
* **Data Analysis with Advanced SQL (`queries.sh`):**
  * Complex aggregations (`AVG`, `SUM`, `COUNT`, `ROUND`).
  * Relational queries with multiple `JOIN`s between team and match tables.
  * Advanced groupings and filters (`GROUP BY`, `ORDER BY`, `LIKE`).
 
## 🛠️ Technologies Used
* **Database:** PostgreSQL
* **Scripting Language:** Bash / Shell Scripting
* **Data Source:** CSV (Comma-Separated Values)

## 🚀 How to Run the Project
### Prerequisites
Have PostgreSQL and the `psql` command-line tool installed.
### Setup Steps
1. **Clone the repository:**
   ```bash
      git clone https://github.com/Akisolu/world-cup-database.git
      cd world-cup-database
   ```
2. **Create and import the base database:**
   ```bash
      psql -U postgres < worldcup.sql
   ```
3. **Give execution permissions to the scripts:**
   ```bash
      chmod +x insert_data.sh queries.sh
   ```
4. **Populate the database from the CSV:**
   ```bash
      ./insert_data.sh
   ```
5. **Run the SQL queries report:**
   ```bash
      ./queries.sh
   ```

## 📊 Analytical Queries Examples
```SQL
   -- Average number of goals scored by winning teams rounded to 2 decimal places
   SELECT ROUND(AVG(winner_goals), 2) FROM games;

   -- Teams that have won the cup (alphabetical order)
   SELECT DISTINCT(name) 
   FROM teams 
   INNER JOIN games ON teams.team_id = games.winner_id 
   WHERE round = 'Final' 
   ORDER BY name;
```

---

## 📜 Credits and Acknowledgments

* **Prompt / dataset origin:** This project is one of the challenges required to obtain the **Relational Database Certification** from [freeCodeCamp](https://www.freecodecamp.org/).
* **Implementation:** The Bash scripting logic (`insert_data.sh`), the structuring of the PostgreSQL schema (`worldcup.sql`), and the development of analytical queries (`queries.sh`) were entirely developed as an individual solution to the proposed problem.
