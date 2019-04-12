# Techedge SQL Database Style Guide

<a href="https://www.techedgegroup.com" target="blank">
    <img src="https://cdn2.hubspot.net/hubfs/500261/assets/img/techedge.svg" width="300">
</a>
<br><br>

**Esta guía de estilo tiene como objetivo dar una pauta para crear bases de datos bajo un estilo unificado .**

## Reglas

* **Usar nombres en inglés** para el nombre de la base de datos, esquemas y columnas.

    ```sql
    CREATE TABLE usuario;     -- ✗ evitar
    CREATE TABLE user;        -- ✓ ok
    ```

* **Usar snake case para** nombrar las columnas.

    ```sql
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        birthDate DATE,              -- ✓ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        birth-date DATE,              -- ✓ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB;  
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        birth_date DATE,              -- ✓ ok
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```

* **Todas las claves foráneas debe finalizar con _id.**

    ```sql
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        profile TINYINT NOT NULL          -- ✓ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        profile_id TINYINT NOT NULL,      -- ✓ ok
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Evitar el uso de composite primary keys.**<br>
Para tener la flexibilidad de extrapolar los datos sobre soluciones basadas en bases de datos noSQL, es recomendable usar una única clave primaria para una mayor compatibilidad.

    ```sql
    CREATE TABLE user (
        section_id INT NOT NULL,
        company_id INT NOT NULL,  
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (section_id, company_id)  -- ✓ evitar
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        section_id INT NOT NULL,
        company_id INT NOT NULL,
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (id)                      -- ✓ ok
    )  ENGINE=INNODB;
    ```
