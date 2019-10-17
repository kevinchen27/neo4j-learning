## Patterns in Cypher
Patterns are the most powerful capability of graphs. Nodes and relationships can express simple or complex patterns. 
<br>
To show a pattern, we combine the node and relationship syntaxes
<br>
Example: Jennifer likes Graphs
<br>
**(p:Person {name: "Jennifer"})-[rel:LIKES]->(g:Technology {type: "Graphs"})**
<br>
<br>
However, we dont tell e Cypher what we want to do with this pattern. To do that we use keywords.

## Cypher Keywords
They convey specific actions in Cypher. 

### MATCH

Searches for an exisitng node, relationship, label, property, or pattern. This is like SELECT in SQL.
<br>

### RETURN

Required for reads but not writes. Specifies what values or results you want to return from a Cypher query.
<br>
Variables need to be references when returning a specific node or relationship

### Examples

1. Find the labeled **Person** nodes in the graph
<br>
**MATCH (p:Person) RETURN p**
<br>
<br>
2. Find person with name Jennifer
<br>
MATCH (p:Person {name: "Jennifer"}) RETURN p
<br>
3. Find which company Jennifer works for
<br>
Structure: We know we need to find Jennifer's Person node, and we need to find the Company nodes she is connected to. Thus, we need WROKS_FOR relatioship to the Company node. We want to return the company that she works for.
<br>
**MATCH (:Person {name: 'Jennifer'})-[:WORKS_FOR]->(company:Company)
RETURN company**
<br>
4. Find the name of the company Jennifer works for
<br>
We use the syntax variable.property to return the name value
<br>
**MATCH (:Person {name: 'Jennifer'})-[:WORKS_FOR]->(company:Company)
RETURN company.name**

## Aliasing Return Values

You rename return results using AS and calling the returned item a better name.
<br>
Example:
<br>
**MATCH (kristen:Customer {name:'Kristen'})-[rel:PURCHASED]-(order:Order)
RETURN order.orderId AS OrderID, order.orderDate AS `Purchase Date`,
       kristen.customerIdNo AS CustomerID, order.orderNumOfLineItems AS `Number Of Items`**
       
 
