# ELT on Postgres databases

This repository contains a custom Extract, Load, Transform (ELT) project that utilizes Docker and PostgreSQL to demonstrate a simple ELT process.

The aim of the project is to understand how dbt, Airflow and Airbyte work.

## Table of Contents
- [Structure](#structure)
- [Usage](#usage)
- [How it Works](#works)

## Structure

1. **docker-compose.yaml**: This file contains the configuration for Docker Compose, which is used to orchestrate multiple Docker containers. It defines three services:

    - **source_postgres**: The source PostgreSQL database.
    - **destination_postgres**: The destination PostgreSQL database.
    - **elt_script**: The service that runs the ELT script.
2. **elt_script/Dockerfile**: This Dockerfile sets up a Python environment and installs the PostgreSQL client. It also copies the ELT script into the container and sets it as the default command.

3. **elt_script/elt_script.py**: This Python script performs the ELT process. It waits for the source PostgreSQL database to become available, then dumps its data to a SQL file and loads this data into the destination PostgreSQL database.

4. **source_db_init/init.sql**: This SQL script initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, and inserts sample data into these tables.

## Usage

1. Have Docker and Docker Compose installed on your machine.
2. Clone this repository.
3. Navigate to the repository directory and run docker-compose up.
4. Once all containers are up and running, the ELT process will start automatically.
5. After the ELT process completes, you can access the source and destination PostgreSQL databases on ports 5433 and 5434, respectively.

## How it works

- Docker Compose: Using the docker-compose.yaml file, three Docker containers are created
- ELT Process: The elt_script.py waits for the source PostgreSQL database to become available. Once it's available, the script uses pg_dump to dump the source database to a SQL file. Then, it uses psql to load this SQL file into the destination PostgreSQL database.
- Database Initialization: The init.sql script initializes the source database with sample data. It creates several tables and populates them with sample data.
