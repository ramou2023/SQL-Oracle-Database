Ce projet à pour objectif l'initialisation à la creation des bases de données et la prise en main des requetes SQL En Utilisantb ORACLE.

**Partie 1 : Installation d'ORACLE**

 1. Telecharger  d'abord l'édition 21c d'Oracle Database(SQL PLus) sur le site officiel d'Oracle
 2. Definir uun mot de passe  pour le nom d'utilisateur "SYSTEM" lors de l'installation du logiciel Oracle Database
 3. Telecharger  ORACLE SQL Developer puis etablir une connection avec a=la base de données en utilisant l'utilisateur SYSTEM et le mot de passe precedement defini.


**Partie 2 :  Creation de la base de données**

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
La base de données creée avec deux tables  aura cette forme:

![image](https://github.com/ramou2023/SQL-Oracle-Database/assets/140972803/6e14deeb-b2d7-435b-bfe1-8fecb739326b)

Pour creer la base de données avec **l'ensemble des tables** , il suffit d'aller executer le fichier `ddl.sql` se trouvant dans le dossier `Source/DDL/`

**Partie 3 :  Data Manipulation Language (DML)**

### Commandes basiques

##### selectionner les données
```
select * from departments;
select * from jobs;
select * from locations;
```
##### ordonner les données après selection
```
select first_name|| ' '||last_name
from employees
order by first_name, last_name;
```
##### appliquer des filtres : selectioonner les employer dont l'id commenace par "AD"
```
select FIRST_NAME, LAST_NAME, EMAIL, JOB_ID
from employees
where job_id LIKE 'AD%';
```

##### Rêquete avec plusieurs conditions 

1.1. job id commençant par AD et salaire >10000
1.2 OU  job id commençant par  IT and salaire <= 6000
2.2 COMMISSION_PCT doit être  0
3.1 hire date doit être après le  1-JAN-1990
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

