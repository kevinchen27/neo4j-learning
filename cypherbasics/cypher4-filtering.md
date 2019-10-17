## Filtering Queries

To retrieve values satisfying a certaon condition, we use filtering queries.
<br>
### WHERE clause

The term WHERE is self-explanatory: you want to find a place WHICH is called Los Angeles for example.
Just substitute WHICH is called for **WHERE** witht he following syntax
<br>
//query using equality check in the MATCH clause
MATCH (j:Person {name: 'Jennifer'})
RETURN j
<br>
//query using equality check in the WHERE clause
MATCH (j:Person)
WHERE j.name = 'Jennifer'
RETURN j

## WHERE NOT

Opposite of WHERE: when you want a query where result IS NOT a certain value.

//query using inequality check in the WHERE clause
MATCH (j:Person)
WHERE NOT j.name = 'Jennifer'
RETURN j

## Ranges of values

Use **<= <item> <=**: just like in math

**MATCH (p:Person)
WHERE 3 <= p.yearsExp <= 7
RETURN p**

## If property exists

To see an observation which has a certain property.
Neo4j does not store null properties. The syntax is WHERE exists(variable.property)

//Query1: find all users who have a birthdate property
MATCH (p:Person)
WHERE exists(p.birthdate)
RETURN p.name

//Query2: find all WORKS_FOR relationships that have a startYear property
MATCH (p:Person)-[rel:WORKS_FOR]->(c:Company)
WHERE exists(rel.startYear)
RETURN p, rel, c

## Querying Strings
Coupled with WHERE clause
- **STARTS WITH** : see if a string starts with a certain letter
//check if a property starts with 'M'
MATCH (p:Person)
WHERE p.name STARTS WITH 'M'
RETURN p.name
- **CONTAIN**: string contains certain characters
3/check if a property contains 'a'
MATCH (p:Person)
WHERE p.name CONTAINS 'a'
RETURN p.name

- **ENDS_WITH**: string ends with certain characters
//check if a property ends with 'n'
MATCH (p:Person)
WHERE p.name ENDS WITH 'n'

You can also use regular expressions:
MATCH (p:Person)
WHERE p.name =~ 'Jo.*'
RETURN p.name

**IN**
<br>
You can also use IN like in SQL but instead we put them in [] brackets

## Filtering patterns

//Query1: find which people are friends of someone who works for Neo4j
MATCH (p:Person)-[r:IS_FRIENDS_WITH]->(friend:Person)
WHERE exists((p)-[:WORKS_FOR]->(:Company {name: 'Neo4j'}))
RETURN p, r, friend
<br>
What's happening is it returns person and friend for which p works for Neo4j

//Query2: find Jennifer's friends who do not work for a company
MATCH (p:Person)-[r:IS_FRIENDS_WITH]->(friend:Person)
WHERE p.name = 'Jennifer'
AND NOT exists((friend)-[:WORKS_FOR]->(:Company))
RETURN friend.name
<br>
Returns friend name when the relationship "friends that works for company" does not exist

