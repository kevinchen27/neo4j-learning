# Neo4j Learning
Neo4j documentation for learning. This documentation assumes prior familiarity with network graph fundamentals. 

# Cypher
Query language used in Neo4j. Allows you to execute commands on network graphs (including creating network graphs)

## Patterns
Cypher works really well with patterns. 

() or (p) represents nodes. p is an alias
<br>
(p:Person:Mammal) - the colon represents labels or tags with which you can group roles or types
<br>
(p:Person {name: 'Veronica'}) - nodes can have properties. PErson is a label, name is a property

## Relationships
Wrapped with hyphens or square brackets
**-->** or **-[h:HIRED]->**

Direction is specified with < or >
(p1)-[:HIRED]->(p2) or (p1)<-[:HIRED]-(p2)
(p2) Aliases or references such that later in the query you can access those references
Eg. In match statement maybe want to use person we found and add additional propoerties

Relationships also have properties
<br>
-[:HIRED {type:'fulltime'})->
