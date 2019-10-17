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
<br>
**(p1)-[:HIRED]->(p2) or (p1)<-[:HIRED]-(p2)**
<br>
**(p2)** Aliases or references such that later in the query you can access those references
<br>
Eg. In match statement maybe want to use person we found and add additional propoerties

Relationships also have properties
<br>
**-[:HIRED {type:'fulltime'})->**

## Basic Create and Query
**CREATE (:Person {name:"Ann"}) -[:LOVES]->(:Person{name:"Dan"})**
Name properties inside {} and love relationship is in between the two people inside arrows
<br>
We create label person with properties "Ann" and loves "Dan"

#### Who does Ann love?
**MATCH (:Person{name:"Ann"}) -[:LOVES]->(op:Person)
RETURN op**
<br>
We use alias to return result of the query

## Adding more properties
**MATCH (:Person{name:"Ann}) -[:DRIVES]->(c:Car)
RETURN c**

#### Second way
**MATCH (a:Person)-[:DRIVES]->(c:Car)**
<br>
**WHERE a.name = 'Ann'**
<br>
**SET c.brand = 'Volvo'**
<br>
**c.model='V70'**
<br>
**RETURN c**
<br> 
The SET command changes the properties of car

### Ensuring Uniqueness
Don't want multiple Ann's. Assume Ann is unique. To esure this, use constraint
**CREATE CONSTRAINT ON (p:person) ASSERT p.name IS UNIQUE**

**CREATE (:Person{name:"Ann"})** - we would get constraint error indicating there's already another label

#### Uniqueness on Create
We don't want to experience this error
<br>
**CREATE (a:Person{name:"Ann"})**
<br>
**CREATE (a)-[:HAS_PET]-> (:Dog {name:"Sam"})**
<br>
<br>
Creating a person and create "has a pet", we would get a constraint validation error again
<br>
<br>
To avoid this, we MERGE. IF it exists, it will merge, if it doesn't, it will create the person
<br>
**MERGE (a:Person {name:"Ann"})**
<br>
**CREATE (a)-["HAS_PET]->(:Dog{name:"Sam"})**
<br>
<br>
Looks in graph for a person named "Ann" and looks for a person named Ann and operates on that person node if it exists. If it does not exist, it will create it

**MERGE (a:Person {name:"Ann"})**
<br>
**ON CREATE SET a.twitter = "@ann"**
<br>
**MERGE (a)-[:HAS_PET]->(:Dog {name:"Sam"})**
<br>
<br>
Find existing person named Ann. If its not found, set Twitter property when creating a node named Ann. The create statement here creates the pet relationship only if the relationship does not already exist in the graph

### Comments
Add comments using // 

## Nodes
Nodes are depicted in parentheses ()
<br>
<br>
You can assign it variables like (p) if we want to refer to the node. More real-world variables are like (person) or (thing)
<br>
() does not allow you to RETURN the node later in the query. Do this only if the nod eis not relevant to your query

### Node Labels
Labels are like tags and llow you to specify certain types of entitites to look for or create.
<br>
Think of it like telling SQL which table to look for a particular row. If no label is specified, it checks all nodes in the database.

### Examples

**()**                 //anonymous node (no label or variable) can refer to any node in the database
<br>
**(p:Person)**          //using variable p and label Person
<br>
**(:Technology)**       //no variable, label Technology
<br>
**(work:Company)**      //using variable work and label Company

## Relationships in Cypher

Represented using --> or <-- between two nodes. Additional information such as relationship type can be placed inside square brackets inside the arrows
<br>
Undirected relationships have --. A direction must be inserted in databse, but it can aslo be matched with undirected relationship (Cypher ignores any particular direction)

//data stored with this direction
<br>
**CREATE (p:Person)-[:LIKES]->(t:Technology)**

//query relationship backwards will not return results
<br>
**MATCH (p:Person)<-[:LIKES]-(t:Technology)**

//better to query with undirected relationship unless sure of direction
<br>
**MATCH (p:Person)-[:LIKES]-(t:Technology)**

### Relationship types
Similar to node labels. Relationship types show how nodes are connected and related to each other. Try and use good conventions when naming relationships
<br>
[:LIKES]
<br>
[:IS_FRIENDS_WITH]

### Relationship variables
To refer to a relationship later in a query, give it a variable like [r] or [rel]. Longer variables like [likes] or [knows] also work. If you don't need to reference the relationship laer, you can specify an anonymous relationship using --, -->, or <--

Example:
<br>
**-[rel]-> or =[rel:LIKES]->** and call the rel variable later in your query to reference the relationship and its details
<br>
**-[LIKES]->**  - forgetting the colon means that Cypher will search all types of relationships
