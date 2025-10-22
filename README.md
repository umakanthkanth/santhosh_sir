# Objective
To design a normalized relational data model that captures employee details

The database is hosted on Neon (PostgreSQL) and connected to Google Looker Studio for building interactive dashboards and data visualizations

Tools & Technologies Used
Component                   Description                      Link
Database Platform Neon – Serverless PostgreSQL instance https://console.neon.tech/app/projects/spring-truth-6417
Database Engine PostgreSQL (latest stable version)
Visualization Tool Google Looker Studio https://lookerstudio.google.com/reporting/61dfa0b7-c376-4a9b-bd43-33f1e90d1ccb
Connection Type Direct PostgreSQL SSL connection
Data Source Sample employee access data created manually

Database Design (ER Model)
The database uses a star-like schema with a central employee_details table connected to multiple child tables
such as ad_groups, git_access, and sop status via foreign keys (user_id). This ensures data normalization and easy scalability.

Tables & Schema
