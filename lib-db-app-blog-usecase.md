---
title: lib-db-app-blog-usecase
tags: [blog, database-design, tree, usecase]
created: 2023-10-26T18:19:36.493Z
modified: 2023-10-26T18:20:15.359Z
---

# lib-db-app-blog-usecase

# guide

# blogs-usecase-tree-hierarchical
- usecase-tree
  - tag
  - comments
  - pages
  - filesystem

- A great overview of the pros and cons of different approaches is given in [Models for hierarchical data | PPT](https://www.slideshare.net/billkarwin/models-for-hierarchical-data)
  - [Persistent tree structure using closure table in MySQL](https://gist.github.com/kovid-rathee/243846cbd140f21aae5b510e51f2aed5)
- [Trees and Hierarchies in SQL | PPT](https://www.slideshare.net/ehildebrandt/trees-and-hierarchies-in-sql)
- [Trees In The Database - Advanced data structures | PPT](https://www.slideshare.net/quipo/trees-in-the-database-advanced-data-structures)
- [SQL Antipatterns: Avoiding the Pitfalls of Database Programming by Bill Karwin](https://pragprog.com/titles/bksqla/sql-antipatterns/)

- [Closure Table Pattern to Model Hierarchies in NoSQL | by Andriy Zabavskyy | Towards Data Science](https://towardsdatascience.com/closure-table-pattern-to-model-hierarchies-in-nosql-c1be6a87e05b)
- [Hierarchical Data cont’d – Path Enumeration and Closure Tables](https://www.codingblocks.net/podcast/episode-29-hierarchical-data-contd-path-enumeration-and-closure-tables/)

## [What are the Options for Storing Hierarchical 分层 Data in a Relational Database? - Francis's Octopress Blog](https://jhjguxin.github.io/blog/2012/04/13/what-are-the-options-for-storing-hierarchical-fen-ceng-data-in-a-relational-database/)

- Adjacency List
  - Cheap node moves, inserts, and deletes.
  - Expensive to find level (can store as a computed column), ancestry & descendants (Bridge Hierarchy combined with level column can solve), path (Lineage Column can solve).
  - Use Common Table Expressions in those databases that support them to traverse.

- Flat Table
  - A modification of the Adjacency List that adds a Level and Rank (e.g. ordering) column to each record.
  - Expensive move and delete
  - Cheap ancestry and descendants
  - Good Use: threaded discussion - forums/blog comments

- Lineage Column (a.k.a. Materialized Path, Path Enumeration)
  - Limit to how deep the hierarchy can be.
  - Descendants cheap (e.g. LEFT(lineage, #) = '/enumerated/path')
  - Ancestry tricky (database specific queries)

- Nested Set (a.k.a Modified Preorder Tree Traversal)
  - Cheap level, ancestry, descendants
  - Compared to Adjacency List, moves, inserts, deletes more expensive.
  - Requires a specific sort order (e.g. created). So sorting all descendants in a different order requires additional work.

- Nested Intervals
  - Combination of Nested Sets and Materialized Path where left/right columns are floating point decimals instead of integers and encode the path information. 
  - In the later development of this idea nested intervals gave rise to matrix encoding.

- Bridge Table (a.k.a. Closure Table: some good ideas about how to use triggers for maintaining this approach)
  - Cheap ancestry and descendants (albeit not in what order)
  - For complete knowledge of a hierarchy needs to be combined with another option.

- MySQL
  - Use session variables for Adjacency List

- Oracle
  - Use CONNECT BY to traverse Adjacency Lists

- PostgreSQL
  - `ltree` datatype for Materialized Path

- SQL Server
  - 2008 offers HierarchyId data type appears to help with Lineage Column approach and expand the depth that can be represented.

## [PostgreSQL and Rails, sitting in a tree_201603](https://evilmartians.com/chronicles/postgresql-and-rails-sitting-in-a-tree)

- Nested Set is the worst option:
  - slowest
  - The most complicated algorithm with complex queries.
  - Has issues with concurrency—updates always require locks.
- Materialized Path is much better:
  - fastest
  - Can be used natively with PostgreSQL.
  - the internals are still complicated.
- Closure Table is something in-between:
  - The easiest algorithm which best fits in with the relational model.
  - Can use foreign keys to maintain referential integrity.
  - No need to modify existing table schema.
  - an extra table is to be created. This table will contain the links between each parent and all its descendants.

## [Storing hierarchical data: Materialized Path – Bojan Živanović](https://bojanz.wordpress.com/2014/04/25/storing-hierarchical-data-materialized-path/)

- Storing the hierarchy in a materialized path requires only one column in the table.
- Storing the hierarchy in a closure table requires an additional table with a large number of rows.
- The closure table also won’t work if you need to sort items by hierarchy, and re-parenting items is slow and costly. On the other hand, it’s normalized, which can’t be said for materialized paths.

## [Tree structure in relational db Symfony](https://www.ekreative.com/blog/tree-structure-in-relational-dbs-theory-and-use-in-symfony/)

- It’s not a new problem, the “parent” problem in tree-based data sets has been around for a long time. Essentially the task is to quickly retrieve a dataset containing parents and children, without resorting to a recursive or massive nested join query.
- There are a number of different approaches to the problem, each involving a different model of hierarchical data implementations. 
  - I found this post very helpful for understanding the **adjacency list** and **nested set** models and the following articles for the **closure tables** and **materialized path** models. 
  - Those are the four main models which I’ll be looking at here.

- 👉🏻 The Adjacency List Model
- This model has each table item contain a pointer to its parent (with the root item having a NULL value for its parent). 
- This is a tricky model to implement with pure SQL as you need to know the level of a category before you can see its full path. 
- Also, there’s a risk of orphaning sub-trees when deleting nodes, so extra care needs to be taken!

```SQL
CREATE TABLE category (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
parent INT DEFAULT NULL
);

INSERT INTO category VALUES
(1,‘Databases’,NULL),
(2,‘Relational’,1),
(3,‘Document’,1),
(4,‘MySQL’,2),
(5,‘PostgreSQL’,2),
(6,‘MongoDB’,3);

-- Retrieving children of parent node
SELECT `id`,`name` FROM `category`
WHERE `category`.`parent` = 2;

```

- 👉🏻 The Materialized Paths model
- a document stores each tree node along with a string of the nodes path. 
- This pattern is more flexible in allowing work with the path, but does involve working with strings and regular expressions.

```SQL
CREATE TABLE category (
name VARCHAR(20) NOT NULL,
path VARCHAR(256) DEFAULT NULL
);

INSERT INTO category VALUES
(‘Databases’, NULL),
(‘Relational’, ‘,Databases,’),
(‘Document’, ‘,Databases,’),
(‘MySQL’, ‘,Databases,Relational,’),
(‘PostgreSQL’, ‘,Databases,Relational,’),
(‘MongoDB’, ‘,Databases,Document,’);

-- Retrieving a Sub-tree Path:
SELECT name FROM category
WHERE path LIKE “,Databases,Relational,%”;

```

- 👉🏻 The Closure Table Model
- all paths from one node in the tree to another are stored. 
- this requires a lot of space, as you are storing a lot more pathing data, but it’s more flexible than something like the Nested Set model in cases where ordering doesn’t matter. 
- we store for each node its “ancestor” (parent), “descendant” (child), and “depth”, which is the level from the tree’s root.

```SQL
CREATE TABLE category (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
parent INT DEFAULT NULL
);

INSERT INTO category VALUES
(1,‘Databases’,NULL),
(2,‘Relational’,1),
(3,‘Document’,1),
(4,‘MySQL’,2),
(5,‘PostgreSQL’,2),
(6,‘MongoDB’,3);

CREATE TABLE category_closure (
ancestor INT DEFAULT NULL,
descendant INT DEFAULT NULL,
depth INT DEFAULT NULL
);

INSERT INTO comment_closure VALUES
(1,1,0),(0,1,0),(2,2,0),(1,2,1),(3,3,0),(1,3,1),(0,3,1),(4,4,0),(2,4,1),(1,4,2),(0,4,2),(5,5,0),(2,5,1),
(1,5,2),(0,5,2),(6,6,0),(3,6,1),(1,6,2),(0,6,2);

-- Retrieving a Sub-tree Path:
SELECT `id`,`parent` FROM `category`
JOIN `category_closure` `closure`
ON `category`.`id` = `closure`.`descendant`
WHERE `closure`.`ancestor` = 2;

```

- 👉🏻 The Nested Set Model
- This model uses an approach called the modified preorder tree traversal algorithm. What this means is that we work from the left to the right of a tree, one layer at a time, descending to each node’s children before assigning a right-hand number and moving on to the right.
- When we use this structure of tree, it is easy for us to select particular nodes, sub-trees, parent sub-trees and others.

```SQL

CREATE TABLE category (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
lft INT NOT NULL,
rgt INT NOT NULL,
lvl INT NOT NULL,
);

CREATE TABLE category (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
lft INT NOT NULL,
rgt INT NOT NULL,
lvl INT NOT NULL,
);

-- We can retrieve the full tree with ordering and levels (where number of *s is the level):
SELECT name, lvl FROM category ORDER BY lft;

-- Retrieving a Sub-tree Path:
SELECT name, lvl FROM category WHERE lft >= 2 AND rgt <= 7 ORDER BY lft;
```

- In Symfony Framework we can use StofDoctrineExtensionsBundle, which implements all the features of DoctrineExtensions

## [Closure Table | The Cache • Fueled Engineering_202105](https://fueled.com/the-cache/posts/backend/closure-table/)

- This post looks at representing and managing hierarchical data structures in a relational database system like PostgreSQL, MySQL using an approach called Closure tables.

- 👉🏻 Adjacency Lists: node-table

```
Hierarchical tree:
    id (pk),
    parent_id (fk) NULL,
    name,
    ...
```

- `parent_id` references another row in the table itself and a foreign key constraint can be added to enforce it at the database level. 
  - The root of the tree has `parent_id` set as `null`.
- This naive approach can do the following operations quite easily:
  - Adding a node to the tree.
  - Finding all immediate children of a node.
  - Finding all siblings of a node.
  - Moving a node anywhere in the tree.
- However, it is not a good approach when your application might need to do the following:
  - Querying all descendants/children of a node.
  - Deleting a node is expensive, you might need to either delete the whole sub-tree

- 👉🏻 Closure Table: node-table + closure-table

```
Node:
    id (pk),
    name,
    ....

Closure Table:
    id (pk),
    parent (fk to node),
    child (fk to node),
    depth
```

- The Closure Table solution is an elegant way of storing hierarchies that trade-off space complexity for query time efficiency. 
  - It involves storing all paths that exist in the tree in a separate table, unlike adjacency lists which only store the parent-child path.
- closure-table stores information about the tree structure.
# blogs

# more
