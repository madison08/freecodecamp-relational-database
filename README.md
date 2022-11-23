# sheet for relationnal database (postgres)

psql --username=freecodecamp --dbname=postgres


sudo -u postgres createuser madison
❯ sudo -u postgres createdb likambo
❯ sudo -u postgres psql

#

CREATE DATABASE first_databse

#

\c datbase_name (connection to databse)
\d (see tables)

#

CREATE TABLE first_table();
CREATE TABLE second_table();


\d second_table;
\d table_name (voir plus d'information sur une table)


#

ALTER TABLE second_table ADD COLUMN first_column INT

ALTER TABLE table_name ADD COLUMN column_name DATATYPE;

#

Ajouter une autre colonne
ALTER TABLE second_table ADD COLUMN id INT;

#

Ajout d'autre colonne
ALTER TABLE second_table ADD COLUMN age INT;

#

Suppression de colonne
ALTER TABLE second_table DROP COLUMN age;

#

Une autre suppression
ALTER TABLE second_table DROP COLUMN first_column;

#

ALTER TABLE second_table ADD COLUMN name VARCHAR(30);

#

Renommer colonne
ALTER TABLE second_table RENAME COLUMN name TO username;

#
Ajouter une ligne dans une table
INSERT INTO second_table(id,username) VALUES(1,'Samus');