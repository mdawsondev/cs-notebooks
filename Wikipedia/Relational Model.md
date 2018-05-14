# Relational Model

The relational model is an approach to managing data using a structure and language consistent with first-order predicate logic¹. A database organized in therms of the relational model is a relational database. The purpose of this model is to provide a declarative method for specifying data and queries. Users state exactly what information the database contains and what they want from it, and the database management system takes care of describing data structures for storing and retrieval.

*Most* relational databases use SQL, implementing what is regarded to as an engineering approximation to the relational model. A **table** in SQL schema corresponds to a predicate variable - the contents of a table to a relation. Key constraints, other constraints, and SQL queries correspond to predicates. Data in a relational model is organized into tables, which are called relations. 👌

_**1: First-order logic** - Quantified variables over non-logical objects to allow the use of sentences that contain variables, so that rather than "Socrates is a man," one can instead say "there exists X such that X is Socrates and X is a man," and `there exists` is a quantifer while `x` is available._

![Relational Model Diagram](https://upload.wikimedia.org/wikipedia/commons/8/8d/Relational_model_concepts.png)

The main concept behind a relational model is that it allows the database designer to create a consistant, logical representation of information. Consistancy is achieved by including declared constraints in the database design, which is referred to as the **logical schema**.

The basic relational building block is the _domain_, or _data type_, usually abbreviated now to _**type**_. A tuple represents an ordered set of attribute values, and an attribute is an ordered pair of the attribute name and type name.

A relation (table) consists of a heading and a body, the heading being a set of attributes, and the body is a set of n-tuples. This works like pretty much any other table, except the data must be accouted for via the schema.

## SQL and the Relational Model

SQL is pushed as the standard language for relational databases, but deviates from the rleational model in several places. SQL is an extention of the relational model design, but it is possible to make a database conforming to the relational model using SQL if certain features are omitted.

The specific deviations from the model are noted in SQL; few database servers implement the entire SQL standard and some do not allow specific deviations. Where NULL is ubiquitous for example, allowing duplicate column names within a table or anonymous colloms is uncommon.

* Duplicate Rows
* Anonymous Columns
* Duplicate Column Names
* Column Order Significance
* Views without CHECK OPTION
* Columnless Tables Unrecognized
* NULL

### Relational Operations

A request is made from a relational database by sending a query written in SQL (or a similar dialect). SQL is usually embeded into the database software that provides an easier UI; many websites such as Wikipedia perform SQL queries when generating pages.

In response to a query the database returns a set, which is just a list of rows containing the answers. The simplest query is just to return all rows from a table, but usualy the rows are filtered in some way to return desired answers.

Often data from multiple tables will be combined into one via `join`. There are a number of relational operation in addition to join, including project, restrict, union, difference, intersect, and product. Depending on the source consulted, there are a number of other operators as well.

## Example

* Customer (**Customer ID**, Tax ID, Name, Address, City, State, Zip, Phone, Email, Sex)
* Order (**Order No**, _Customer ID_, _Invoice No_, Date Placed, Date Promised, Terms, Status)
* Order Line (**Order No**, **Order Line No**, _Product Code_, Qty)
* Invoice (**Invoice No**, _Customer ID_, _Order No_, Date, Status)
* Invoice Line (**Invoice No**, **Invoice Line No**, _Product Code_, Qty Shipped)
* Product (**Product Code**, Product Description)

In this design there are six revlars (relation variables): Customer, Order, Order Line, Invoice, Invoice Line, and Product. The bold attribute are candidate keys, the italicised attributes are foreign keys.

Usually, one candidate key is chosen to be called the **primary key** and used in preference over the other candidate keys, which are often then called alternate keys. A candidate key is a unique identifier enforcing that *no rows will be duplicated*. Both foreign keys and superkeys (including candidate key) can be composed of several attributes.