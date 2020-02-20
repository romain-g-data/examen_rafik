partie 1 -REQUETE SQL 
----------------------

**1**

	from re import sub


liste = 'code (insee)	mode de scrutin	numliste	code (nuance de la liste)	numéro du candidat dans la liste	tour	nom	prénom	sexe	Date de naissance	code (profession)	libellé profession	nationalité' 


		def r_names(liste):
		    listepropre  = sub('[é,è]','e',liste)
		    listepropre1 = sub('[., ,\']','_',listepropre)
		    listepropre2 = sub('[(,)]','',listepropre1)
		    listepropre3 = listepropre2.split('\t') 
		    
		    return listepropre3
		
		print(r_names(liste))





**2**

listepropre3 =r_names(liste)

def parse_dates(listepropre3):
    for i in range (0, len(listepropre3)):
        if listepropre3[i][0:4]=='Date':
            return listepropre3[i]

print(parse_dates(listepropre3))



partie 2 -REQUETE SQL 
----------------------


**3**

CREATE DATABASE KNE;

USE KNE







**4**
------



CREATE TABLE IF NOT EXISTS KNE.`categorie` (
  `idcategorie` INT(11) NOT NULL,
  `Code` INT(5) NULL,
  `Nb d'emplois au lieu de travail (LT) 2016` VARCHAR(6) NULL,
  `Artisans, commerçants, chefs d'entreprise` VARCHAR(6) NULL,
  `Cadres et professions intellectuelles supérieures` VARCHAR(6) NULL,
  `Professions intermédaires` VARCHAR(6) NULL,
  `Employés` VARCHAR(6) NULL,
  `Ouvriers` VARCHAR(6) NULL,
  PRIMARY KEY (`idcategorie`))

DEFAULT CHARACTER SET = latin1;


CREATE TABLE IF NOT EXISTS `KNE`.`departements` (
  `iddepartements` INT(11) NOT NULL,
  `region_code` VARCHAR(5) NULL,
  `code_` VARCHAR(5) NULL,
  `name` VARCHAR(45) NULL,
  `nom_normalisé` VARCHAR(45) NULL,
  PRIMARY KEY (`iddepartements`))

DEFAULT CHARACTER SET = latin1;


CREATE TABLE IF NOT EXISTS `KNE`.`elus` (
  `idelus` INT(11) NOT NULL,
  `code_insee` VARCHAR(5) NULL,
  `mode_de_scrutin` VARCHAR(14) NULL,
  `numliste` VARCHAR(2) NULL,
  `code_nuance_de_la_liste` VARCHAR(6) NULL,
  `numero_du_candidat_dans_la_liste` VARCHAR(6) NULL,
  `tour` VARCHAR(1) NULL,
  `nom` VARCHAR(45) NULL,
  `prenom` VARCHAR(45) NULL,
  `sexe` VARCHAR(1) NULL,
  `Date_de_naissance` DATETIME NULL,
  `code_profession` VARCHAR(4) NULL,
  `libelle_profession` VARCHAR(40) NULL,
  `nationalite` VARCHAR(1) NULL,
  PRIMARY KEY (`idelus`))

DEFAULT CHARACTER SET = latin1;


CREATE TABLE IF NOT EXISTS `KNE`.`nuancier` (
  `nu_id` INT(11) NOT NULL,
  `nu_code` VARCHAR(45) NULL,
  `nu_libelle` VARCHAR(45) NULL,
  `nu_ordre` VARCHAR(45) NULL,
  `nu_definition` VARCHAR(300) NULL,
  PRIMARY KEY (`nu_id`))

DEFAULT CHARACTER SET = latin1;


CREATE TABLE IF NOT EXISTS `KNE`.`population` (
  `idpopulation` INT(11) NOT NULL,
  `code_` VARCHAR(45) NULL,
  `Population légale 2017` INT(15) NULL,
  PRIMARY KEY (`idpopulation`))

DEFAULT CHARACTER SET = latin1;


CREATE TABLE IF NOT EXISTS `KNE`.`villes` (
  `vi_id` INT(11) NOT NULL,
  `vi_department_code` VARCHAR(5) NULL,
  `vi_insee_code` VARCHAR(5) NULL,
  `vi_zip_code` VARCHAR(6) NULL,
  `vi_name` VARCHAR(45) NULL,
  PRIMARY KEY (`vi_id`))

DEFAULT CHARACTER SET = latin1;


**5**
------
***CREATE USER 'RNE_user'@'localhost' IDENTIFIED BY 'RNE_pasword';
GRANT ALL PRIVILEGES ON KNE  TO 'RNE_user'@'localhost';
FLUSH PRIVILEGES;***



**6**


from sqlalchemy import create_engine
import pandas as pd
import time

engine = create_engine("mysql+pymysql://root:@localhost/KNE")

def importxls(link, table):
    print("Lecture des données")
    start_time = time.time()
    df = pd.read_excel(link , skiprows=0, header=1)
    print("Données lu")

    df.to_sql(table, con = engine, if_exists='replace', index = False)

    return print("Temps d execution : %s secondes ---" % (time.time() - start_time))


importxls('/home/utilisateur/Documents/evaluation rafik/elus_mun2014.xlsx', 'elus')


partie 3 -REQUETE SQL 
----------------------

**8**

select libelle from nuancier where libelle like "%union%";



**9**

**10**









