# Databases | Neo4j & Cypher {ignore=true}

By **Stephan Djurhuus**
Institute **CPHBusiness**

Education **Software Development**
Elective **Databases**
Topic **Graph Databases**

**Important Resources**
* [Getting Started](https://neo4j.com/developer/get-started/)
* [Operations Manual](https://neo4j.com/docs/operations-manual/4.0/)
* [Cypher Manual](https://neo4j.com/docs/cypher-manual/4.0/)

## Content {ignore=true}
[TOC]

## Neo4j

### General Information
Neo4j is a highly scalable native graph database, purpose-built to leverage not only data but also data relationships.

Using Neo4j, developers build intelligent applications that traverse today's large, interconnected datasets in real time. Powered by a native graph storage and processing engine, Neo4j delivers an intuitive, flexible and secure database for unique, actionable insights.

_Unlike other databases, Neo4j connects data as it is stored, enabling it to traverse connections orders-of-magnitude faster._

_[reference, neo4j.com](https://neo4j.com/neo4j-graph-database/)_

#### Functionality
Neo4j stores and displays data in the form of graph. In Neo4j, data is represented by nodes and relationships between those nodes.

Neo4j databases (as with any graph database) are a lot different to relational databases such as MS Access, SQL Server, MySQL, etc. Relational databases use tables, rows, and columns to store data. They also present data in a tabular fashion.

Neo4j doesn't use tables, rows, or columns to store or present data.

Neo4j is best for storing data that has many interconnecting relationships that's why graph databases like Neo4j has an advantage and much better at dealing with relational data than relational databases are.

The graph model doesn't usually require a predefined schema. So there is no need to create the database structure before you load the data (like you do in a relational database). In Neo4j, the data is the structure. Neo4j is a "schema-optional" DBMS.

In Neo4j, no need to set up primary key/foreign key constraints to predetermine which fields can have a relationship, and to which data. You just have to define the relationships between the nodes you need.

_[reference, javatpoint.com](https://www.javatpoint.com/neo4j-tutorial/)_

#### ACID
ACID is a set of properties that guarantee database transactions are processed reliably and a transaction is a single logical operation on the database.

**Atomicity** requires that a transaction is all or nothing, which means if a portion of a transaction fails, the state of the database is left without changes.

**Consistency** ensures any transactional operation will leave the database at a consistent state as defined by constraints, etc applied to the database.

**Isolation** guarantees concurrent transactions will execute as if they were performed sequentially requiring that within a transaction, altered data won’t be accessed by other operations prior to commit.

**Durability** means that once a transaction has been committed it will remain even if the database crashes immediately thereafter.

To completely preserve integrity of data while ensuring adequate transactional behavior, Neo4j supports properties of ACID and below is a quick overview of some of the specific implementation:

* Database operations accessing the indexes, graph, or schema should be carried out within a transaction.
* READ_COMMITTED is the default isolation level.
* Data taken by traversals isn’t shielded from modification from other transactions.
* Non-repeated reads could happen (example: write locks are only acquired and held until the end point of a transaction).
* Write locks can be acquired manually on relationships and nodes to acquire higher isolation level.
* Locks can be acquired only at the node and relationship level.
* Detection of deadlock is created into the transaction management core.

_[reference, graphgrid.com](https://www.graphgrid.com/neo4j-is-designed-to-be-your-source-of-truth-database/)_

#### Normalization
The graph data model is often referred to as being “whiteboard-friendly”. Typically, when designing a data model, people draw example data on the whiteboard and connect it to other data drawn to show how different items connect. The whiteboard model is then re-formatted and structured to fit normalized tables for a relational model.

A similar process exists in graph data modeling, as well. However, instead of modifying the data model to fit a normalized table structure, the graph data model stays exactly as it was drawn on the whiteboard. This is where the graph data model gets its name for being “whiteboard-friendly”.

_[reference, neo4j.com](https://neo4j.com/developer/guide-data-modeling/)_

#### Advantages

**Highly Scalable**
Neo4j is highly scalable. It provides a simple, powerful and flexible data model which can be changed according to applications and uses. It provides:

* Higher vertical scaling.
* Improved operational characteristics at scale.
* Higher concurrency.
* Simplified tuning.

**Schema Free**
Neo4j is schema-free like other NoSQL databases.

**High Availability**
Neo4j provides high availability for large enterprise real-time applications with transactional guarantees.

**Real-time Data Analysis**
Neo4j provides results based on real-time data.

**Easy Representation**
Neo4j provides a very easy way to represent connected and semi-structured data.

**Fast Execution**
Neo4j is fast because more connected data is very easy to retrieve and navigate.

**Easy Retrieval**
Neo4j facilitates you not only represent but also easily retrieve (traverse/navigate) connected data faster other databases comparatively.

**Cypher Query language**
Neo4j provides CQL (_Cypher Query Language_) a declarative query language to represent the graph visually, using ASCII-art syntax. The commands of this language is very easy to learn and human readable.

**No Join**
Neo4j doesn't require complex Joins to retrieve connected/related data as it is very easy to retrieve its adjacent node or relationship details without Joins or Indexes because it is a graph database and all nodes are already connected.

_[reference, javatpoint.com](https://www.javatpoint.com/advantages-of-neo4j)_

#### Disadvantages
**Where data is disconnected and relationships do not matter**
If you have transactional data and do not care how it relates or connects to other transactions, people, etc, then graph is probably not the solution.

**Where optimizing for writing and storing data and do not need to read or query it**
If the use case is only looking to write data to the store and not expecting to analyze or query results, then graph may not solve the problem.

**Where core data objects or data model stay consistent and data structure is fixed and tabular**
If you have constant, unchanging types of data that you are collecting, then graph may not be the most appropriate solution. Graphs are well-suited to storing any or all elements and can easily adapt to changing business and data capture needs.

**Where queries execute bulk data scans or do not start from a known data point**
If your queries are doing table scans to find a match or searching for data that fits a general category, then a graph solution is not best-suited to the task. A graph database is built and optimized for traversing relationships from a starting data point or set. It is not optimized for searching the entire graph without a specific starting point or set in mind.

**Where you will use it as a key-value store**
If you are only interested in a lookup operation, then a graph database is not the solution for you. As we have discussed above, graph analysis benefits from relationships among data. A lookup result from a known key does not maximize the function of what graph databases were created to do.

**Where large amounts of text or BLOBS need to be stored as properties**
If you are storing and retrieving entity properties that contain extremely large values (such as BLOBs, CLOBs, text paragraphs, etc), then another technology solution might be a better choice. Graph databases are very good at traversing relationships between small data entities, but not ideally suited to store a lot of properties on a single node or large values in those properties. The reason for this is because the query can hop from entity to entity at top speed, but then also needs extra processing to pull out the details of each entity it finds along a path.

_[reference, medium.com](https://medium.com/neo4j/how-do-you-know-if-a-graph-database-solves-the-problem-a7da10393f5)_

### Graph Database
In computing, a graph database (GDB) is a database that uses graph structures for semantic queries with nodes, edges, and properties to represent and store data. A key concept of the system is the graph (or edge or relationship). The graph relates the data items in the store to a collection of nodes and edges, the edges representing the relationships between the nodes. The relationships allow data in the store to be linked together directly and, in many cases, retrieved with one operation. Graph databases hold the relationships between data as a priority. Querying relationships within a graph database is fast because they are perpetually stored within the database itself. Relationships can be intuitively visualized using graph databases, making them useful for heavily inter-connected data.

Graph databases portray the data as it is viewed conceptually. This is accomplished by transferring the data into nodes and its relationships into edges. A graph within graph databases is based on graph theory. It is a set of objects, either a node or an edge.

#### Nodes, (_Vertex_)
Represent entities or instances such as people, businesses, accounts, or any other item to be tracked. They are roughly the equivalent of a record, relation, or row in a relational database, or a document in a document-store database.

#### Relationships, (_Edge_)
Are the lines that connect nodes to other nodes; representing the relationship between them. Meaningful patterns emerge when examining the connections and interconnections of nodes, properties and edges. The edges can either be directed or undirected. In an undirected graph, an edge from a point to another has one meaning. In a directed graph, the edges connecting two different points have different meanings depending on their direction. Edges are the key concept in graph databases, representing an abstraction that is not directly implemented in a relational model or a document-store model.

#### Properties
Are information germane to nodes. For example, if Wikipedia were one of the nodes, it might be tied to properties such as website, reference material, or words that starts with the letter w, depending on which aspects of Wikipedia are germane to a given database.

_[reference, wikipedia.org](https://en.wikipedia.org/wiki/Graph_database)_

### GraphQL
GraphQL is a specification for querying a slice of an application graph, retrieving a tree of data that perfectly matches a front-end view, regardless of where that data was pulled from. It covers tree-based read queries, mutations for updates, and subscriptions for live updates.

#### GRANDstack
GRANDstack is a full-stack development integration for building graph-based applications.

**GraphQL** is a query language for APIs and a runtime for fulfilling those queries with your existing data

**React** is a JavaScript library for building user interfaces

**Apollo Client** is a fully-featured, production-ready caching GraphQL client for every server or UI framework

**Neo4j Database** is a graph database that is ACID-compliant and built to store and retrieve connected data

_[reference, neo4j.com](https://neo4j.com/developer/graphql/)_

## Cypher

### General Information
Cypher is Neo4j’s graph query language that allows users to store and retrieve data from the graph database. 

Cypher’s syntax provides a visual and logical way to match patterns of nodes and relationships in the graph. It is a declarative, SQL-inspired language for describing visual patterns in graphs using ASCII-Art syntax. It allows us to state what we want to select, insert, update, or delete from our graph data without a description of exactly how to do it. Through Cypher, users can construct expressive and efficient queries to handle needed create, read, update, and delete functionality.

_[reference, neo4j.com](https://neo4j.com/developer/cypher-query-language/)_

### Syntax

### Data Types

### CRUD Operations

#### Create
#### Read
#### Update
#### Delete

### Advanced Operations

#### Conditions
#### Transactions
#### Functions
#### Aggregations

### Cypher Shell

#### Setup Shell Aliases
https://neo4j.com/download-center/#cyphershell
https://neo4j.com/developer/kb/how-do-i-authenticate-with-cypher-shell-without-specifying-the-username-and-password-on-the-command-line/

_shell_
```shell
open -t ~.zprofile
```

Change `<USERNAME>` to the corresponding username on your computer.

_.zprofile_
```shell

```

_shell_
```shell
source ~.zprofile
```

#### Shell Commands

**Start Console**
```shell
neo4j console
```

**Start Database**
```shell
neo4j start
```

**Stop Database**
```shell
neo4j stop
```

**Status Database**
```shell
neo4j status
```

**Restart Database**
```shell
neo4j restart
```

**Version Database**
```shell
neo4j version
```

#### Load External Data

_[reference, neo4j.com](https://neo4j.com/docs/operations-manual/current/tools/cypher-shell/)_

## Examples

### JavaScript

_[reference, neo4j.com](https://neo4j.com/developer/javascript/)_

### Python

_[reference, neo4j.com](https://neo4j.com/developer/python/)_

