# dw_task

**Start time**: 11.08.2024 - 18:30  
**End time**: 11.08.2024 - 21:30

## Initial Steps:

1. **Installed Homebrew on Mac.**
2. Brew wasn't working though it was installed because the path was not set. The path was set using the following command:
    ```bash
    echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
    ```
   (For Apple silicon Mac)
3. **PostgreSQL Installation**: 
    ```bash
    brew install postgresql
    ```
4. **Initializing the database**: 
    ```bash
    brew services start postgresql
    ```
5. **Accessing the PostgreSQL interactive terminal**: 
    ```bash
    psql postgres
    ```
6. **Create a new user** (if you want a user other than postgres):
    ```sql
    CREATE USER shakh WITH PASSWORD '123456';
    ```
7. **Create a new database**: 
    ```sql
    CREATE DATABASE dw_database;
    ```
8. **Grant privileges to the user**: 
    ```sql
    GRANT ALL PRIVILEGES ON DATABASE dw_database TO shakh;
    ```
9. **Exit the PostgreSQL shell**: 
    ```bash
    \q
    ```
10. **Creating a Conda Environment**: 
    ```bash
    conda create --name dw_env python=3.8
    ```
    (Miniconda was installed before) & activating conda environment: 
    ```bash
    conda activate dw_env
    ```
11. **Installed pandas, SQLAlchemy, psycopg2**: 
    ```bash
    pip install pandas sqlalchemy psycopg2
    ```
12. **Checking DataFrame**: using Pandas.
13. **PgAdmin4 was installed.**
14. **Testing database connection using Python.**
15. **Upload data to the Database.**

## Approach

### Data Ingestion:
- Process begins by raeding social media reports in CSV format into a Pandas DataFrame.
- Columns are renamed for consistency, with spaces replaced by underscores and text converted to lowercase.
- Missing values (NaN) are replaced with `None` to ensure compatibility with the PostgreSQL database.

### Database Schema Design:
- A PostgreSQL database is used to store the processed data.
- Three tables were designed: `facebook_pages`, `page_statistics`, and `posts`, each holding relevant data extracted from the reports.

### Data Cleaning and Transformation:
- Data is cleaned by converting text fields to lowercase, removing commas from numeric strings, and converting time fields to seconds.
- Boolean values are standardized, converting 'Yes'/'No' to True/False.
- Missing values in key columns are handled by filling them with default values (e.g., 0 for interaction metrics).

### Data Insertion:
- Data is inserted into the PostgreSQL database using the `to_sql` method from SQLAlchemy, which handles bulk inserts efficiently.

### Feature Engineering:
- Additional features such as engagement rate and time-of-day categorization are derived from the raw data for more insightful analysis.

## Challenges Encountered

### Data Integrity:
- Ensuring data consistency across different tables, especially when handling missing or malformed data, required careful preprocessing.

### Time Conversion:
- Converting time strings to a numerical format (seconds) for easier analysis required custom functions to handle edge cases.

### Error Handling and Logging:
- Implementing robust error handling to manage database connection issues, data inconsistencies, and other potential problems.

## Pipeline Architecture

### Data Ingestion:
- CSV reports are read into Pandas DataFrames, with initial cleaning and transformation done in-memory.

### Database Layer:
- A PostgreSQL database is used to store data in a normalized schema with three main tables.

### Data Transformation:
- Data is cleaned and transformed within the DataFrame before being inserted into the database.

### Feature Engineering:
- New features such as engagement rate and time-of-day categorization are computed before inserting data into the database.

## Reasons Behind Choices

### PostgreSQL Database:
- Chosen for its robustness, support for complex queries, and ease of integration with Python via SQLAlchemy.

### Pandas for Data Transformation:
- Offers powerful tools for data cleaning and transformation, making it ideal for handling CSV input and preparing data for insertion.

### SQLAlchemy for Database Interaction:
- Provides a flexible and powerful ORM that simplifies database operations and supports efficient data insertion.

## Further Ideas

### Automation and Scheduling:
- Implementing a task scheduler (Not implemented) to automate the daily processing of reports. (Example: Here is only a CSV has been processed)

### Real-time Data Processing:
- Exploring real-time data streaming and processing solutions for handling social media data as it arrives.

### Dashboard Integration:
- Direct integration with business intelligence tools (e.g., Power BI, Tableau) to visualize the processed data.

### Enhanced Error Handling and Logging:
- Implementing comprehensive logging to track processing steps and handle errors more effectively.

### Archiving Processed Reports:
- archiving processed reports to cloud storage or a dedicated directory for future reference.

### Scalability Improvements:
- Optimizing the pipeline to handle even larger data sets(Possibly using distributed data processing)

### Code Improvements:
- Using OOP to handle the whole process easily.



## Diagrams:

- UML Diagram has been added in Diagram folder
- ER Diagram has been added in Diagram folder