<img width="733" height="1204" alt="image" src="https://github.com/user-attachments/assets/50e86e0b-f4ed-429b-9b7a-233958e1b03d" /># Objective
To design a normalized relational data model that captures employee details

The database is hosted on Neon (PostgreSQL) and connected to Google Looker Studio for building interactive dashboards and data visualizations

#Tools & Technologies Used
Component                   Description                      Link
Database Platform Neon – Serverless PostgreSQL instance https://console.neon.tech/app/projects/spring-truth-6417
Database Engine PostgreSQL (latest stable version)
Visualization Tool Google Looker Studio https://lookerstudio.google.com/reporting/61dfa0b7-c376-4a9b-bd43-33f1e90d1ccb
Connection Type Direct PostgreSQL SSL connection
Data Source Sample employee access data created manually

Database Design (ER Model)
The database uses a star-like schema with a central employee_details table connected to multiple child tables
such as ad_groups, git_access, and sop status via foreign keys (user_id). This ensures data normalization and easy scalability.

#Tables & Schema
Table "public.employee_details"
Column	Type	Collation	Nullable	Default
user_id	character varying(50)		not null	
resource_name	character varying(100)			
manager_name	character varying(100)			
onboarding_status	character varying(30)			
product_team	character varying(100)			
role	character varying(100)			
email_id	character varying(150)			
query_input	character varying(20)			
sop_status	character varying(20)			
Indexes:
"employee_details_pkey" PRIMARY KEY, btree (user_id)
Referenced by:
TABLE "ad_group_access" CONSTRAINT "ad_group_access_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE

Table "public.sop_status"
Column	Type	Collation	Nullable	Default
sop_id	integer		not null	nextval('sop_status_sop_id_seq'::regclass)
user_id	character varying(50)			
sop_name	character varying(100)			
sop_completion_status	character varying(50)			
Indexes:
"sop_status_pkey" PRIMARY KEY, btree (sop_id)
Foreign-key constraints:
"sop_status_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE

Table "public.ad_group_access"
Column	Type	Collation	Nullable	Default
ad_access_id	integer		not null	nextval('ad_group_access_ad_access_id_seq'::regclass)
user_id	character varying(50)			
ad_group_type	character varying(50)			
ad_group_name	character varying(100)			
access_status	character varying(80)			
Indexes:
"ad_group_access_pkey" PRIMARY KEY, btree (ad_access_id)
Foreign-key constraints:
"ad_group_access_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE

Table "public.git_access"
Column	Type	Collation	Nullable	Default
git_access_id	integer		not null	nextval('git_access_git_access_id_seq'::regclass)
user_id	character varying(50)			
access_type	character varying(50)			
access_status	character varying(80)			
Indexes:
"git_access_pkey" PRIMARY KEY, btree (git_access_id)
Foreign-key constraints:
"git_access_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE


Data Normalization
Normalization applied up to 3rd Normal Form (3NF): ensuring atomic values (1NF), dependency on primary
key (2NF), and no transitive dependency (3NF). This design minimizes redundancy and ensures scalability.

Connection to Looker Studio
Looker Studio was connected to Neon PostgreSQL using SSL, selecting the unified view to build visual
dashboards.

Summary
Successfully created a normalized PostgreSQL database on Neon, linked to Google Looker Studio, and
visualized access data with clean, scalable structure.
 Dashboard: https://lookerstudio.google.com/reporting/61dfa0b7-c376-4a9b-bd43-33f1e90d1ccb
 Neon Database: https://console.neon.tech/app/projects/spring-truth-64178874/auth
TABLE "git_access" CONSTRAINT "git_access_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE
TABLE "sop_status" CONSTRAINT "sop_status_user_id_fkey" FOREIGN KEY (user_id) REFERENCES employee_details(user_id) ON DELETE CASCADE
