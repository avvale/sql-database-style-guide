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

* **Usar snake case** para nombrar las columnas.

    ```sql
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        birthDate DATE,              -- ✗ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        birth-date DATE,              -- ✗ evitar
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
        profile INT NOT NULL          -- ✗ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        profile_id INT NOT NULL,      -- ✓ ok
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
        PRIMARY KEY (section_id, company_id)  -- ✗ evitar
    )  ENGINE=INNODB; 
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        section_id INT NOT NULL,
        company_id INT NOT NULL,
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (id)                      -- ✓ ok
    )  ENGINE=INNODB;
    ```
    
* **Usar id** como denominación para la clave primaria, siendo siempre un autoincrement o UUID.<br>
Para tener la flexibilidad de extrapolar los datos sobre soluciones basadas en bases de datos noSQL, es recomendable usar una única clave primaria para una mayor compatibilidad.

    ```sql
    CREATE TABLE user (
        ID INT AUTO_INCREMENT,            -- ✗ evitar
        NAME VARCHAR(255) NOT NULL,
        PRIMARY KEY (ID)
    )  ENGINE=INNODB;
  
    CREATE TABLE user (
        _id INT AUTO_INCREMENT,            -- ✗ evitar
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (_id)
    )  ENGINE=INNODB;
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,            -- ✓ ok
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Usar el prefijo 'is' o 'has'** en las columnas booleans.

    ```sql
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        active TINYINT(1) NOT NULL,       -- ✗ evitar
        purchase TINYINT(1) NOT NULL      -- ✗ evitar
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
  
    CREATE TABLE user (
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        is_active TINYINT(1) NOT NULL,       -- ✓ ok
        has_purchase TINYINT(1) NOT NULL     -- ✓ ok
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Usar uppercase** para la sintaxis SQL.

    ```sql
    create table user (                   -- ✗ evitar
        id int AUTO_INCREMENT,
        name varchar(255) not null,
        primary key (id)
    )  engine=innodb;
  
    CREATE TABLE user (                   -- ✓ ok
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```

* **Usar los siguietnes sufijos** para nominar las constraints.

    * **primary key:** _pk
    * **foreign key:** _fk
    * **check:** _ck
    * **not null:** _nn
    * **unique:** _uq
    * **index:** _idx
    
* **Usar el siguiente patrón** para nominar las constraints.

    ```
    <tablename>_<columnname>_<suffix>
    ```
    
* **Usar singular** para denominar a la tabla

    ```sql
    CREATE TABLE users (                  -- ✗ evitar
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,       
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
  
    CREATE TABLE user (                   -- ✓ ok
        id INT AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,       
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Usar plural** para denominar a las tablas relacionales

    ```sql
    CREATE TABLE user_profile (                 -- ✗ evitar
        id INT AUTO_INCREMENT,
        user_id INT NOT NULL,
        profile_id INT NOT NULL,       
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
  
    CREATE TABLE users_profiles (                   -- ✓ ok
        id INT AUTO_INCREMENT,
        user_id INT NOT NULL,
        profile_id INT NOT NULL,       
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Usar el sufijo i18n** para denominar a las tablas de internacinalización

    ```sql
    CREATE TABLE product_lang (                 -- ✗ evitar
        id INT AUTO_INCREMENT,
        common_id INT NOT NULL,
        lang_id VARCHAR(2) NOT NULL,  
        name VARCHAR(255) NOT NULL,     
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
  
    CREATE TABLE product_i18n (                 -- ✓ ok
        id INT AUTO_INCREMENT,
        common_id INT NOT NULL,
        lang_id VARCHAR(2) NOT NULL,  
        name VARCHAR(255) NOT NULL,    
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
    
* **Usar el prefijo param** para denominar a las tablas de parametrización

    ```sql
    CREATE TABLE mail_parameter (             -- ✗ evitar
        id INT AUTO_INCREMENT,
        smtp VARCHAR(255) NOT NULL,  
        pop VARCHAR(255) NOT NULL,
        imap VARCHAR(255) NOT NULL,     
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
  
    CREATE TABLE param_mail (                 -- ✓ ok
        id INT AUTO_INCREMENT,
        common_id INT NOT NULL,
        smtp VARCHAR(255) NOT NULL,  
        pop VARCHAR(255) NOT NULL,
        imap VARCHAR(255) NOT NULL,     
        PRIMARY KEY (id)
    )  ENGINE=INNODB;
    ```
