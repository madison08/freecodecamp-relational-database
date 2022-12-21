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

`ALTER TABLE second_table ADD COLUMN name VARCHAR(30);`

#

Renommer colonne
ALTER TABLE second_table RENAME COLUMN name TO username;

#
Ajouter une ligne dans une table
INSERT INTO second_table(id,username) VALUES(1,'Samus');

#
SELECT * FROM second_table;

#
INSERT INTO second_table(id, username) VALUES(2,'Mario');

#
INSERT INTO second_table(id, username) VALUES(3, 'Luigi');
#
Supprimmer une ligne
DELETE FROM second_table WHERE username='Luigi';

#
voir detail de table
\d second_table;

# 
Supprimer la colonne d'une table
ALTER TABLE second_table DROP COLUMN username;

#
supprimer une table
DROP TABLE second_table;

#
voir les base de donnees
\l

#
modifier le nom d'une base de donnee
ALTER DATABASE first_database RENAME TO mario_database;

#
supprimer une base de donnee
DROP DATABASE second_database;

#
create table
CREATE TABLE characters();


#
add table
ALTER TABLE characters ADD COLUMN character_id SERIAL;

(serial rend notre  colonne entier, non null, et auto incrementer)


#
add table
ALTER TABLE characters ADD COLUMN name VARCHAR(30) NOT NULL;

#
add table
ALTER TABLE characters ADD COLUMN homeland VARCHAR(60);
#
add row
INSERT INTO characters(name, homeland, favorite_color) VALUES('Mario','Mushroom Kingdom','Red');

#
add multi row
INSERT INTO characters(name, homeland, favorite_color) VALUES('Toadstool','Mushroom Kingdom','Red'),('Bowser','Mushroom Kingdom','Green') 

#
add multi row
INSERT INTO characters(name, homeland, favorite_color) VALUES('Daisy','Sarasaland','Yellow'),('Yoshi','Dinosaur Land','Green');

#
update column in row
UPDATE characters SET favorite_color='Orange' WHERE name='Daisy';

#
update column in row
UPDATE characters SET name='Toad' WHERE favorite_color='Red';

#
update column
UPDATE characters SET name='Mario' WHERE character_id=1;

#
update column
UPDATE characters SET favorite_color='Blue' WHERE name='Toad';

#
data by order
SELECT columns FROM table_name ORDER BY column_name;
SELECT * from characters ORDER BY character_id;

#
set primary key
ALTER TABLE table_name ADD PRIMARY KEY(column_name);
ALTER TABLE characters ADD PRIMARY KEY(name);

#
drop constraint
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
ALTER TABLE characters DROP CONSTRAINT characters_pkey;

#
create table
CREATE TABLE more_info();

#
set foreign key
ALTER TABLE table_name ADD COLUMN column_name DATATYPE REFERENCES referenced_table_name(referenced_column_name)
ALTER TABLE more_info ADD COLUMN character_id INT REFERENCES characters(character_id);

#
add unique constraint
ALTER TABLE table_name ADD UNIQUE(column_name);
ALTER TABLE more_info ADD UNIQUE(character_id);

#
set NOT NULL constraint
ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;
ALTER TABLE more_info ALTER COLUMN character_id SET NOT NULL;
#

#
show column from table
SELECT character_id FROM characters;

#
show columns
SELECT character_id,name FROM characters;

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1981-07-09',155,64.5,1);

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1983-07-14',175,48.8,2);

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1985-10-18',173,52.2,3);

#
select with condiions
SELECT columns FROM table_name WHERE condition;
SELECT character_id,name FROM characters WHERE name='Toad';

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1950-01-10',66,35.6,4);

#
select specific row
SELECT character_id,name FROM characters WHERE character_id=5;

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1990-10-29',258,300,5); 

#
find row
SELECT character_id,name FROM characters WHERE character_id=6;

#
insert with except some column
INSERT INTO more_info(birthday,character_id) VALUES('1989-07-31',6);

#
find row
SELECT character_id,name FROM characters WHERE character_id=7;

#
insert
INSERT INTO more_info(birthday,height,weight,character_id) VALUES('1990-04-13',162,59.1,7);

#
rename column
ALTER TABLE more_info RENAME COLUMN height TO height_in_cm;

#
rename column
ALTER TABLE more_info RENAME COLUMN weight TO weight_in_kg;

#
create table
CREATE TABLE table_name();

#
create table and add column
CREATE TABLE table_name(column_name DATATYPE CONSTRAINTS);
CREATE TABLE sounds(sound_id SERIAL PRIMARY KEY);

#
add column
ALTER TABLE sounds ADD COLUMN filename VARCHAR(40) NOT NULL UNIQUE;

#
add foreign key
ALTER TABLE table_name ADD COLUMN column_name DATATYPE CONSTRAINT REFERENCES referenced_table_name(referenced_column_name);
ALTER TABLE sounds ADD COLUMN character_id INT NOT NULL REFERENCES characters(character_id);

#
insert row
INSERT INTO sounds(filename,character_id) VALUES('its-a-me.wav',1);

#
multiple insert
INSERT INTO sounds(filename,character_id) VALUES('yay.wav',3),('woo-hoo.wav',3);

#
create table
CREATE TABLE actions(action_id SERIAL PRIMARY KEY);

#
add column
ALTER TABLE actions ADD COLUMN action VARCHAR(20) NOT NULL UNIQUE;

#
insert
INSERT INTO actions(action) VALUES('run');

#
create table
CREATE TABLE character_actions();

#
add column
ALTER TABLE character_actions ADD COLUMN character_id INT NOT NULL;

#
add foreign key existing column
ALTER TABLE table_name ADD FOREIGN KEY(column_name) REFERENCES referenced_table(referenced_column);
ALTER TABLE character_actions ADD FOREIGN KEY(character_id) REFERENCES characters(character_id);

#
add column
ALTER TABLE character_actions ADD COLUMN action_id INT NOT NULL;

#
add foreign key
ALTER TABLE character_actions ADD FOREIGN KEY(action_id) REFERENCES actions(action_id);

#
create primary key with composite column
ALTER TABLE table_name ADD PRIMARY KEY(column1, column2);
ALTER TABLE character_actions ADD PRIMARY KEY(character_id,action_id);

#
multiple insert
INSERT INTO character_actions(character_id,action_id) VALUES(7,1),(7,2),(7,3);

#
select with join 
SELECT columns FROM table_1 FULL JOIN table_2 ON table_1.primary_key_column = table_2.foreign_key_column;

SELECT * FROM characters FULL JOIN more_info ON characters.character_id = more_info.character_id;

#
select with join
SELECT * FROM characters FULL JOIN sounds ON characters.character_id = sounds.character_id;

#
select with 3 tables join // jonction table
SELECT columns FROM junction_table
FULL JOIN table_1 ON junction_table.foreign_key_column = table_1.primary_key_column
FULL JOIN table_2 ON junction_table.foreign_key_column = table_2.primary_key_column;

SELECT * FROM character_actions
FULL JOIN characters ON character_actions.character_id = characters.character_id
FULL JOIN actions ON character_actions.action_id = actions.action_id;

