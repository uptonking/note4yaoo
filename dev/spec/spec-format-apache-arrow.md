---
title: spec-format-apache-arrow
tags: [apache-arrow, format, spec]
created: 2021-07-24T08:14:04.860Z
modified: 2021-07-24T08:14:45.182Z
---

# spec-format-apache-arrow

# guide

# blogs

# pandas

- [pandas 2.0 and the Arrow revolution (part I)](https://datapythonista.me/blog/pandas-20-and-the-arrow-revolution-part-i)
  - Python data structures (lists, dictionaries, tuples, etc) are very slow and can't be used.
  - For many years, the main extension to represent arrays and perform operations on them in a fast way has been NumPy. And this is what pandas was initially built on.
  - While NumPy has been good enough to make pandas the popular library it is, it was never built as a backend for dataframe libraries, and it has some important limitations. 
    - A couple of examples are the poor support for strings and the lack of missing values.
    - For some years now, while still relying heavely on NumPy, pandas has been slowly decoupling from it.
    - A couple of important milestones were the addition of an API to implement Extension Arrays for pandas in 2018.
    - Another important milestone was the implementation of a string data type based on Arrow that started in 2020.
# changelog

## [Introducing ADBC: Database Access for Apache Arrow_202301](https://arrow.apache.org/blog/2023/01/05/introducing-arrow-adbc/)

- introduce version 1.0.0 of the Arrow Database Connectivity (ADBC) specification. 
  - ADBC is a columnar, minimal-overhead alternative to JDBC/ODBC for analytical applications. 
  - Or in other words: ADBC is a single API for getting Arrow data in and out of different databases.

### Motivation

- Applications often use API standards like JDBC and ODBC to work with databases.
  - That way, they can code to the same API regardless of the underlying database, saving on development time.
- Roughly speaking, when an application executes a query with these APIs:
  1. The application submits a SQL query via the JDBC/ODBC API.
  2. The query is passed on to the driver.
  3. The driver translates the query to a database-specific protocol and sends it to the database.
  4. The database executes the query and returns the result set in a database-specific format.
  5. The driver translates the result into the format required by the JDBC/ODBC API.
  6. The application iterates over the result rows using the JDBC/ODBC API.

- When columnar data comes into play, however, problems arise. 
  - JDBC is a row-oriented API, and while ODBC can support columnar data, the type system and data representation is not a perfect match with Arrow. 
  - So generally, columnar data must be converted to rows in step 5, spending resources without performing “useful” work.
- This mismatch is problematic for columnar database systems, such as ClickHouse, Dremio, DuckDB, and Google BigQuery. 
- Row-oriented database systems like PostgreSQL aren’t going away, and these clients will still want to consume data from them.
- Developers have a few options:
  - Just use JDBC/ODBC. converting data into rows for JDBC/ODBC, only for the client to convert them right back into columns! Performance suffers
  - Use JDBC/ODBC-to-Arrow conversion libraries.like Turbodbc and arrow-jdbc. But this doesn’t fundamentally solve the problem. Unnecessary data conversions are still required.
  - Use vendor-specific protocols. But client applications that want to support multiple database vendors would need to integrate with each of them. 

### Introducing ADBC

- ADBC is an Arrow-based, vendor-neutral API for interacting with databases. 
- Applications that use ADBC simply receive Arrow data. 
- Just like JDBC/ODBC, underneath the ADBC API are drivers that translate the API for specific databases.
