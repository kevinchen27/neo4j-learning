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

