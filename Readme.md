Ce projet à pour objectif l'initialisation à la creation des bases de données et la prise en main des requetes SQL En Utilisantb ORACLE.

##Partie 1 : Installation d'ORACLE
 1. Telecharger  d'abord l'édition 21c d'Oracle Database(SQL PLus) sur le site officiel d'Oracle
 2. Definir uun mot de passe  pour le nom d'utilisateur "SYSTEM" lors de l'installation du logiciel Oracle Database
 3. Telecharger  ORACLE SQL Developer puis etablir une connection avec a=la base de données en utilisant l'utilisateur SYSTEM et le mot de passe precedement defini.


##Partie 2 :  Creation de la base de données
Avant de manipuler les bases de données SQL, il faut creer ces bases données en definisant un modele de données. Pour creer les bases de données nous utilisons les requetes DDL à savoir CREATE, UPDATE, ALTER, INSERT,...

Exemple de creation d'une base de données SQL:

```
CREATE TABLE locationsBis
  (locationb_id NUMBER(4),
  street_adressb VARCHAR2(40),
  postal_codeb VARCHAR2(12),
  cityb VARCHAR2(30) CONSTRAINT loc_city_nnb NOT NULL
  );
  
CREATE UNIQUE INDEX loc_id_pkb
    ON locationsBis(locationb_id);
    
ALTER TABLE locationsBis
  ADD (
     CONSTRAINT loc_id_pkb 
     PRIMARY KEY (locationb_id)
  );
CREATE SEQUENCE locationsBis_seq
   START WITH 3300
   INCREMENT BY 100
   MAXVALUE 9900
   NOCACHE
   NOCYCLE;
Create table departmentsBis
     (departmentb_id NUMBER(4),
     departmentb_name VARCHAR2(30) CONSTRAINT dept_name_nnb not NULL,
     managerb_id NUMBER(6),
     locationb_id NUMBER(4)
     );
Create unique index dept_id_pkb
    ON departmentsBis (departmentb_id);

ALTER TABLE departmentsBis
    ADD ( 
        CONSTRAINT dept_id_pkb PRIMARY KEY (departmentb_id),
        CONSTRAINT dept_loc_fkb FOREIGN KEY (locationb_id) 
                  REFERENCES locationsBis(locationb_id)
    );
    
CREATE SEQUENCE departmentsBis_seq
   START WITH 280
   INCREMENT BY 10
   MAXVALUE 9990
   NOCACHE
   NOCYCLE;
```
La base de données creée aura cette forme:\n

![image](https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/6e14deeb-b2d7-435b-bfe1-8fecb739326b)


