+++
title = "Target 1 Accessing data"
description = ""
weight = 1
+++

## Choose data access technologies

Existing options:

1. ADO.NET
2. EF
3. WCF Data services

Decision points:

1. Performance
2. Security 
3. Scalability 
4. Flexibility 
5. Depend
6. Connected vs disconnected
    + Connections are expensive to create (incurs in network usage).
    + Connection are a limited resource on the server side.
    + May cause locks

### ADO.NET

**Characteristics**

+ Secure
+ Performant
+ Scalable (pooling conection approach)
+ Flexible
+ Compatible (Sql Server, oracle, OleDB, ODBC, ...)
+ Data providers:
    - IDbConnection: DbConnection
    - IDbCommand: DbCommand
    - IDataReader: DbDataReader
    - IDbDataAdapter: DbDataAdapter
    - DataSet
    - DataTable

**DataAdapter vs datareader**

+ Datareader is much faster.
+ Datareader provide an async api while dataAdapter provide only sync API.
+ DataAdapter populates only datasets and datatables not custom entities.
+ Both offer multiple datasets retrieval but only dataset lets you mimic a relational database behabiour with for example foreign keys.
+ DataAdapter fill completes only when the ful set of data has been retrieved this allows to get the number of records by using Count().
+ Datareader can be iterated only once and in a forward-omly fashion.
+ Dataset can be loaded from XML file and persisted to XML natively
+ Dataset and dataTable are serializable.

**Why should I choose ADO.NET**

+ Consystency
+ Stability
+ Easyness
+ Compatibility
+ Documentation

### EF
Provides the mean for a developer to focus on application code, not the underlaying plumbing code.

**Origins**

1. LINQ
2. ORM solves Impedance mismatch
3. LINQ-to-SQL
4. EF.

#### EF Modeling
**Structure**

Made of three parts:
1. Conceptual model (conceptual schema definition language CSDL)
2. Data storage aspect (Store Schema Definition Language SSDL)
3. Mapping between conceptual model and data storage (Mapping Specification Language MSL)

**Building**
Two approaches:
1. Database first
2. Model first
3. Code first

#### Beneficts

1. Productivity.
1. Conceptuality.
2. Clear separation of concerns.
3. Data store independency.
4. Compatible with WCF.



## Caching
## Transaction
## Data storage in azure
## WCF data services 
