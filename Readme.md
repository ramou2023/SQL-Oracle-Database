Ce projet a pour objectif la création des bases de données et la manipulation des requêtes SQL en utilisant ORACLE.

**Partie 1 : Installation d'ORACLE**

 1. Telecharger  d'abord l'édition 21c d'Oracle Database(SQL Plus) sur le site officiel d'Oracle
 2. Definir un mot de passe  pour le nom d'utilisateur `SYSTEM` lors de l'installation du logiciel Oracle Database
 3. Telecharger  ORACLE SQL Developer puis etablir une connection avec la base de données en utilisant le nom d'utilisateur `SYSTEM` et le mot de passe précedement defini.


**Partie 2 :  Creation de la base de données**
Avant de travailler avec les bases de données SQL, il est essentiel de créer ces bases de données en établissant un modèle de données. Pour réaliser cette création, nous utilisons les **requêtes DDL** telles que `CREATE`, `UPDATE`, `ALTER`, `INSERT`, etc.

Voici un exemple concret de création d'une base de données SQL :

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
-- INSERTION DES DONNEES 
INSERT INTO locationsBis VALUES 
   ( 1000 
   , '1297 Via Cola di Rie'
   , '00989'
   , 'Roma'
   );
INSERT INTO locationsBis VALUES 
   ( 2400 
   , '93091 Calle della Testa'
   , '10934'
   , 'Venice'
   );
   
INSERT INTO departmentsBis VALUES 
   ( 30
   , 'Purchasing'
   , 114
   , 1000
   );
   
   INSERT INTO departmentsBis VALUES 
   ( 40
   , 'Human Resources'
   , 203
   , 2400
   );

```
La base de données établie, comprenant deux tables, aura la structure suivante :

![image](https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/6e14deeb-b2d7-435b-bfe1-8fecb739326b)

Afin de mettre en place la base de données incluant **toutes les tables**, il vous suffit d'exécuter le fichier  `ddl.sql` qui se situe dans le répertoire `Source/DDL/`.

<img width="263" alt="image" src="https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/a93e6315-4ffb-457b-a031-d5794b4df13e">



**Partie 3 :  Data Manipulation Language (DML)**

#### 3.1 :  Commandes basiques

##### Selectionner les données
```
select * from departments;
select * from jobs;
select * from locations;
```
##### Ordonner les données après selection
```
select first_name|| ' '||last_name
from employees
order by first_name, last_name;
```
##### Appliquer des filtres : selectionner les employés dont l'id commence par "AD"
```
select FIRST_NAME, LAST_NAME, EMAIL, JOB_ID
from employees
where job_id LIKE 'AD%';
```

##### Rêquete avec plusieurs conditions 

Conditions :
- job id commençant par AD et salaire >10000
- OU  job id commençant par  IT and salaire <= 6000
- COMMISSION_PCT doit être  0
- Hire Date doit être après le  1-JAN-1990
```
SELECT * 
FROM EMPLOYEES
WHERE (
(JOB_ID LIKE 'AD%' AND SALARY > 10000)
OR (JOB_ID LIKE 'IT%' AND SALARY <= 10000)
)
OR (
DEPARTMENT_ID IN (90, 60, 30)
AND COMMISSION_PCT = 0
)
AND HIRE_DATE > TO_DATE('1-JAN-2000', 'dd-MON-yyyy');
```
![image](https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/0665d219-5615-4499-b02f-922b9f87b8f7)

##### Commande pour modifier un element dans une table
```
UPDATE EMPLOYEES
set EMAIL = 'rd@gmail.com'
WHERE EMPLOYEE_ID=100;
```
![image](https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/c053233a-a44b-468b-ac0b-cdf6f2a3c47c)

Après une modification, il faut executer la **commande suivante** pour que la modification soit prise en compte:
```
COMMIT;
```

Si on excute pas la commande `commit;`, nous pouvons perdre les modifications quand on fera un rollback `ROLLBACK`;

NB : Vous trouverer des commandes DML dans le dossier `Source/DML` : **Data_Analysis_Part_1.sql** et **Data_Analysis_Part_2.sql**

#### 3.2 : SQL Joins
