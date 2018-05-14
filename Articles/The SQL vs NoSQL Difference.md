# The SQL vs NoSQL Difference: MySQL vs MongoDB

Notes taken from Xplenty's post [The SQL vs NoSQL Difference](https://medium.com/xplenty-blog/the-sql-vs-nosql-difference-mysql-vs-mongodb-32c9980e67b2).

## Big Picture Differences

### Language

**SQL databases** use structured query language (SQL) for defining and manipulating data. SQL is one of the most widely-used options available, but can be very restrictive. It requires that you use predefined schemas to determine the structure of your data before working with it. Additionally, all of the data must follow the same structure. This means that any change in structure could and would be potentially difficult and distruptive to your whole system.

**NoSQL databases** use a dynamic schema for unstructured data, and the data can be stored in many ways: colum-oriented, document-oriented, graph-based, or organized as a KeyValue store. This means you can create documents without first having to define their structure, each document can have a unique structure, the syntax can vary from database to database, and you can append new fields as you go.

### Scalability

In most cases, SQL databases are vertically scalable meaning you can increase the load on a single server by increasing things like CPU, RAM, or SSD. NoSQL databases are horizontally scalable, this means you have to handle higher volumes of traffic by "sharding," or adding more servers in the database. This means that NoSQL databases can grow larger than their original intent, making them the preferred choice for large or constant-changing data sets.

### The Structure

SQL databases are table-based, while NoSQL databases are document-based, key-value pairs, graph databases, or wide-column stores. This means SQL databases are better for storing data that require muilti-row transations of fixed data, such as a banking system, or for legacy systems built for a relational structure.

## SQL vs NoSQL: MySQL vs MongoDB

_Aside: this article dived into MySQL and MongoDB exclusively. I chose to take notes here because they are by far the two most popular that I have had prior experience with._

### MySQL: The Relational Database

* Maturity: MySQL is extremely established, has a huge community, and extensive testing.
* Compatability: MySQL works on all major platforms and has connectors to a large number of languages, meaning it's not limited to SQL.
* Cost-Effective: Open source and free.
* Replicable: Databases can be replicated across nodes allowing workload to be reduced and improving scalability and availability.
* Sharding: Sharding typically can't be done on SQL databases, but it can be done on MySQL servers.

### MongoDB: The NoSQL Non-Relational Database

* Dynamic Schema: Flexibility to change data schema without modifying existing data.
* Scalability: Horizontally scalable to help reduce workload.
* Manageability: Does not require a database administrator, and is much more user-friendly.
* Speed: High-performance for simple queries.
* Flexability: New columns or fields are simple to implement without affecting existing rows or performance.

## Picking a Database

MySQL is a strong choice for businesses benefiting from its pre-defined structure and set schema. Applications that require multi-row transactions like accounting systems or inventory monitoring thrive on MySQL structures.

MongoDB is a good choice for businesses that have rapid growth or no clear schema definitions. It's kind of like working with an object, rather than a table. Specifically, if you can't define a schema and find yourself denormalizing data schemas, or if the schema continues to change (which is often the case with mobile apps, real-time analytics, CMS, etc), MongoDB is the way to go.