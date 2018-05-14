# Relational Database

A digital database based on the relational model of data. A software system used to maintain relational databases is a _relational database management system_. Virtually all relational databases use SQL.

The model organizes data into one or more tables with a unique key (primary) identifying each row (also called records or tuples). Columns are also known as attributes. Typically each table represents one "entity type" (e.g. consumer or product). The row represents instances of that type (such as "Lee" or "chair"), and the columns represent values attributed to that instance (such as address or price).

## Keys and Relations

Each row in a table has a unique (primary) key - rows can be linked to rows in other tables by adding a column for the unique key of the linked row. This is known as a **foreign key**. When a new row is written to the table, a new unique value for the primary key is generated. System performance is optimized for primary keys. Primary keys are used to define the relationships amog tables; when a primary key migrates to another table, it becomes a foreign key in the latter.

**Relationships** are the connection between different tables established on the basis of interaction among tables.

A relation is a set of rows that have the same attributes. The data usually represents an object and information about the object - typically physical or conceptual. This relation is usually described as a table. The relational model specifies that rows of a relation have no specific order and in turn impose no order on attributes. Applications access the data by specifying queries, using operations such as `select` to identify a row, `project` to identify an column, `join` to combine tables. Tables can be modified using `insert`, `delete`, and `update` operators. New rows can supply explicit values or be derived from a query.

Often relations will be queried and joined with other relations, which are called **derived relations**. This can be used as an abstraction layer.

## Constraints

Constraints make it possible to restrict the domain on an attribute (values of a column). For example, you can restrict a given integer to values between 1 and 10. Constraints are one method of implementing business rules in a database and support data use within the application layer. SQL also implements constraint functionality in the form of "check constraints". These are usually defined using expressions that result in a boolean value indicating whether the data satisfies the constraint. They can apply to single attributes, a row, or an entire table.

### Primary Key

A primary key specifies a row within a table - these keys must be unique. While natrual attributes are sometimes good keys, surrogate keys are often a better choice. A surrogate key is an artificial attribute assigned to an object which gives it a unique identity. This key has no intrinsic meaning, but rather is useful through the ability to give a unique key.

Another common occurance is a composit key - a key made up of two or more attributes within a table that together identify a record.

### Foreign Key

A foreign key is a field in a relational table that matches the primary key column of another table. The foreign key is used to cross-reference tables. They do not need to have unique values in referencing, and they effectively use the values of attributes in the referenced table to restrict the domain of one or more attributes in the referenced table.

This can be described as: "For all tuples in the referencing table projected over the referencing columns, there must exist a row in the referenced relation projected over those same columns such that the value in each of the referencing columns matches the corresponding values in the referenced columns."

### Stored Procedures

A stored procedure is a script associated with and generally stored in the database. They usually collect and customize common operations like putting a new row into a table, gathering information about use patterns, or encapsulating complex business logic. Frequently they are used as an API for security or simplicity. Implementations of stored procedures on SQL RDBMS's often allow devs to take advantage of procedural extensions to the standard SQL syntax.

### Index

Indexes are a way of providing quicker access to data - they can be created on any combination of attributes on a table. Queries that filter using those attributes can find matching rows randomly using the index without having to check each row internally. This is similar to using the "index of a book" to go directly to the page with the information you want rather than reading one page at a time. Relational databases usually supply multiple indexing techniques to optomize the combination of data distribution, table size, and typical access patterns.