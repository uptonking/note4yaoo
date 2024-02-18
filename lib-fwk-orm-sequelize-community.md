---
title: lib-fwk-orm-sequelize-community
tags: [community, sequelize]
created: 2023-02-05T18:49:33.768Z
modified: 2023-02-05T18:49:43.540Z
---

# lib-fwk-orm-sequelize-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Table partitioning](https://github.com/sequelize/sequelize/issues/7673)

- > 针对pg的方案有pr，但未合并

- as far as I know none of the NodeJS ORMs show a proper implementation of partitioning and still require more steps to implement it
  - I like to take this since I personally always work with the databases partition stuff, each databases should have different what-to partitioned
  - the complex part is what the partition types is used for partitioning
  - we can implement this feature in Sequelize for every dialects.
  - partitionBy with `sequelize.literal` looks good, but since there is dialects which require more steps to finish a partitioned table, I think we need to create a new interface.

- ## ActiveRecord should be studied more. 
- https://twitter.com/stopachka/status/1715018851249745946
  - It gets a bad rep, mainly because of how meta-programming works in Ruby, but that doesn't detract from how elegant the resulting DSL is.
  - I really like how ActiveRecord does a) validations and b) callbacks
- 
- 

# discuss
- ## 

- ## 

- ## 
