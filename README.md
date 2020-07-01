#### Introduction

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

In this project, we would perform the role of a data engineer, and create a Postgre SQL database that can store music data.



#### Database Design

The database has a star scheme with one fact table and four dimension tables.

* Fact table: 
1. songplays - records in log data associated with song plays i.e. records with page NextSong
   songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent


* Dimension Tables
1. users - users in the app
   columns in users: user_id, first_name, last_name, gender, level

2. songs - songs in music database
   columns in songs song_id, title, artist_id, year, duration

3. artists - artists in music database
   columns in artists: artist_id, name, location, latitude, longitude

4. time - timestamps of records in songplays broken down into specific units
   columns in time: start_time, hour, day, week, month, year, weekday


Due to relately simple data structure of song data (i.e. no or limited many-to-many relationships within data), star schema (instead of snowflake schema) has been chosen for this project.



#### Pipeline Methodology

The challenge of this project is to load two sources of JSON formatted data into a Postgre SQL database. Database client tools (such as DBeaver) may have built-in functions that help developers to load data into database. However, to effectively automate the whole ETL process, it is better to leverage the programming power of Python.

The final pipeline contain three pieces of Python codes:

create_tables.py: this code provides the code structure (i.e. another piece of code would do the actual work) for creating database and table, as well as dropping tabls (so that we don't need to worry about what have been down in the past).

sql_queries.py: this code is actually the unsung hero in this project, because it does all the key works for both create_tables.py and etl.py. As an anology, sql_queries.py would do all the hard work without drawing attention, whereas create_tables.py and etl.py would ask direct help from it; in other words, it's like create_tables.py and etl.py are presenting the glorioius results and claiming all credits in meetings, whereas in effect it is sql_queries.py doing all the major works.

etl.py: this code provides the code structure for extracting, transforming and loading JSON data for the project; again, it is sql_queries.py that actually does the hard work behind the scene.



#### Software Requirements

Python version 3.6.3 and PostgreSQL verion 90521 were used in this project.
