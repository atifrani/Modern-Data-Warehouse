# Projet module architecture BI:  

Chaque jour, des milliers d'entreprises et de particuliers se tournent vers LinkedIn à la recherche de talents.  
Le jeux de données que vous allez explorer contient plus de 33 000 offres d’emploi.  
Pour pouvoir interagir avec les différents jeux de données aux formats fichiers csv et json. Vous allez commencer par charger chaque fichier dans une table de base de données PostgreSQL (utilisez la base de données PostgreSQL créée lors du dernier cours).  

Les fichiers sont dans un bucket S3 public s3://snowflake-lab-bucket/. 


## Chargement des données:

Voici la liste des étapes pour charger les données dans une base de données Snowflake :

1. créez une nouvelle base de données "linkedin"

2. Créez un stage qui spécifie l'emplacement du bucket S3.  

3. Créez les files formats qui correspondes à la structure de données à charger

4. Créez les différentes tables de données.  
voici la description des colonnes de chaque fichier:  

**Jobs_posting :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|job_id                    | The job ID as defined by LinkedIn (https://www.linkedin.com/jobs/view/{job_id})|
|company_id	               | Identifier for the company associated with the job posting (maps to companies.csv)  |
|title	                   | Job title  |
|description	           |     Job description  |
|max_salary	               | Maximum salary  |
|med_salary	               | Median salary  |
|min_salary	               | Minimum salary  |
|pay_period	               | Pay period for salary (Hourly, Monthly, Yearly)  |
|formatted_work_type	   |     Type of work (Fulltime, Parttime, Contract)  |
|location	               | Job location  |
|applies	               |     Number of applications that have been submitted  |
|original_listed_time	   | Original time the job was listed  |
|remote_allowed	           | Whether job permits remote work  |
|views	                   | Number of times the job posting has been viewed  |
|job_posting_url	       |     URL to the job posting on a platform  |
|application_url	       |     URL where applications can be submitted |  
|application_type	       | Type of application process (offsite, complex/simple onsite)  |
|expiry	                   | Expiration date or time for the job listing  |
|closed_time	           |     Time to close job listing  |
|formatted_experience_level	Job | experience level (entry, associate, executive, etc)  |
|skills_desc	           |    Description detailing required skills for job  |
|listed_time	           |   Time when the job was listed  |
|posting_domain	           | Domain of the website with application  |
|sponsored	               |Whether the job listing is sponsored or promoted  |
|work_type	               | Type of work associated with the job  |
|currency	               | Currency in which the salary is provided  |
|compensation_type	       | Type of compensation for the job  |
|scraped	               |     Has been scraped by details_retriever  |


**Salaries :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|salary_id	|The salary ID|
|job_id	The |job ID (references jobs table)|
|max_salary	|Maximum salary|
|med_salary	|Median salary|
|min_salary	|Minimum salary|
|pay_period	|Pay period for salary (Hourly, Monthly, Yearly)|
|currency	|Currency in which the salary is provided|
|compensation_type	|Type of compensation for the job (Fixed, Variable, etc)|
|salary_id	|The salary ID|


**Benefits :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|job_id	|The job ID|
|type	|Type of benefit provided (401K, Medical Insurance, etc)|
|inferred	|Whether the benefit was explicitly tagged or inferred through text by LinkedIn|


**Companies :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|company_id	|The company ID as defined by LinkedIn|
|name	|Company name|
|description	|Company description|
|company_size	|Company grouping based on number of employees (0 Smallest - 7 Largest)|
|country	|Country of company headquarters|
|state	|State of company headquarters|
|city	|City of company headquarters|
|zip_code	|ZIP code of company's headquarters|
|address	|Address of company's headquarters|
|url	|Link to company's LinkedIn page|


**Skills :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|skill_abr	|The skill abbreviation (primary key)|
|skill_name	|The skill name|


**Employee_counts :**  

|Column |                      Description  |
|--------|-----------------------------------|  
|company_id	The |company ID|
|employee_count	|Number of employees at company|
|follower_count	|Number of company followers on LinkedIn|
|time_recorded	|Unix time of data collection|


**Job_Skills :**  

|Column |                      Description  |
|--------|-----------------------------------| 
|job_id	|The job ID (references jobs table and primary key)|
|skill_abr	|The skill abbreviation (references skills table)|


**Industries :**  

|Column |                      Description  |
|--------|-----------------------------------| 
|industry_id	|The industry ID (primary key)|
|industry_name	|The industry name|



**Job_Industries :**  

|Column |                      Description  |
|--------|-----------------------------------| 
|job_id	|The job ID (references jobs table and primary key)|
|industry_id	|The industry ID (references industries table)|


**Company_specialities :**  

|Column |                      Description  |
|--------|-----------------------------------| 
|company_id	|The company ID (references companies table and primary key)|
|speciality	|The speciality ID|


**Company_industries :**  

|Column |                      Description  |
|--------|-----------------------------------| 
|company_id	|The company ID (references companies table and primary key)|
|industry	|The industry ID|


5. Chargez les données dans tables.  

6. Effectuez les transformation nécessaires pour rendre les données exploitable


## Analyse des données:

Avec autant de données, le potentiel d'exploration de cet ensemble de données est vaste et comprend l'exploration des titres d’emploi, des entreprises et des emplacements les mieux rémunérés et examiner comment les industries et les entreprises varient en fonction de leurs offres de emploi/stages et de leurs avantages.  

Une fois que vous avez correctement chargé les fichiers dans votre base de données, vous allez pouvoir commencez à les analyser et répondre à quelques questions :  

1.	Quel est le top 10 de job titles les plus postés ?  
2.	Quel est le job titles les mieux rémunéré (tenir compte de la devise) ?  
3.	Quelle est la réparation des offres d’emploi par taille d’entreprise ?  
4.	Quelle est la réparation des offres d’emploi par type d’industrie ?  
5.	Quelle est la réparation des offres d’emploi par type d’emploi (full-time, intership, part-time) ?  
6.	Toute nouvelle suggestion d’analyse est la bienvenue et sera considérée comme un bonus.  

##  Visulalisation  des données:
Pour chaque question ci-dessus, affichez le résultat sous forme d'un graphique en utlisant streamlit.
Votre web app streamlit, doit contenir pour chaque graphique un titre "au dessus du graphique" et les données utlisées en dessous du graphique.


## Livrable:

Le livrable attendu pour ce projet est un document qui détaille chaque étape du projet :
-	Les commande SQL utilisées.  
-	Le problèmes/erreurs rencontrées.  
-	La solution mise en place pour corriger/résoudre le problème/erreur.  
-   le code python de votre application streamlit.  
-   des commentaires pour expliquer chaque étapes.  

Le travail doit être réalisé par groupe de 5 et la charge répartie de manière équitable entre les membres du groupe.  
Les groupes qui me fourniront des livrables identiques seront sanctionnés.   
