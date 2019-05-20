# Unstructured datasets in Autonomous Database - JSON 

## JSON data has often been stored in NoSQL databases such as Oracle NoSQL Database and Oracle Berkeley DB. These allow for storage and retrieval of data that is not based on any schema, but they do not offer the rigorous consistency models of relational databases.
## To compensate for this shortcoming, a relational database is sometimes used in parallel with a NoSQL database. Applications using JSON data stored in the NoSQL database must then ensure data integrity themselves. Plus, SQL and relational databases provide flexible support for complex data analysis and reporting, as well as rock-solid data protection and access control. This is typically not the case for NoSQL databases, which have often been associated with schemaless development with JSON in the past. 
## Native support for JSON by Oracle Database obviates such workarounds. It provides all of the benefits of relational database features for use with JSON, including transactions, indexing, views and declarative querying, for example in Oracle Database you can use SQL to join JSON data with relational data. And you can project JSON data relationally, making it available for relational processes and tools. You can also query, from within the database as well as JSON data that is stored outside Oracle Database in an external table.##
## And, you can access JSON data stored in the database the same way you access other database data, including using OCI, .NET, and JDBC.

## In Oracle Database, JSON data is stored using the common SQL data types VARCHAR2, CLOB, and BLOB (unlike XML data, which is stored using abstract SQL data type XMLType). 

## In general, you will perform the following tasks when working with JSON data in Oracle Database: 
1. You create internal table, which is the traditional way – where data is stored internally within the database or you create External tables which allow Oracle to query data that is stored outside the database in flat files. You can store these files in either Oracle’s Object Storage, Amazon S3 or Microsoft Azure Blob.
2. create a JSON column with an ”is json” check constraint, Oracle recommends that you use an is_json check constraint to ensure that column values are valid JSON instances 
3. insert JSON data into the column, and 
4. query the JSON data.

## You can also create a database table of JSON data from the content of a JSON dump file.
