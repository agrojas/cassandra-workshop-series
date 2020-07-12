# Week 1

## Class 1
https://www.youtube.com/watch?v=y4Gt_LQ8sdA 

### Notes

- Cassandra is a distributed database.
- Its implemented by severals nodes.
- A node contains resources (RAM,DISK,throughput)
- Nodes use GOSSIPING protocol to communicated beetween them



- Cada nodo puede comunicarse con otro nodo. 
- No hay nodos con roles especificos
- Los nodos estan conectados atraves de un anillo en el datacenter
- Cassandra permite escalar de manera lineal
- Los datos se encuentran distribuidos dentro de los nodos automaticamente. Se utiliza una partition key como elemento para disernir en que nodo se distribuye cada dato
- Permite replicacion automatica
- Cualquier nodo puede handlear el request, en ese momento se vuelve un nodo coordinador. Todos los nodos se conocen entre si, entonces el nodo coordinador sabe a que nodo pertenece este dato (utilizando la partition key) 
- Dependiendo de el valor utilizado en el replication factor, se replicará la data en N nodos (siendo N el replica factor) cuando se grabe un nuevo dato. 
- La replicación tiene multiples beneficios como:
   - Si se cae un nodo, los datos no se pierden ya que se encuentran en los otros.
   - Es mas rápida la lectura ya que varios nodos pueden responder a la solicitud de un dato. Podía verse como un load balancer naturalmente
   - Cuando un nodo caido vuelve a levantarse, se sincroniza nuevamente.
   - El valor estandar es RF=3

#### CAP Theorem


Consistency, Availability, Partition Tolerance

En un sistema distribuido, en el caso de una falla solo se pueden garantizar 2 de las 3 cualidades

Cassandra por default es un AP system --> garantiza Availability y Partition Tolerance
(Aunque puede configurarse para CP system, lo bueno de esto es que puede configurarse por query)


Consistency levels and replication factor
**RF = 3**
- CL=ONE: alcanza con que uno de los nodos replica responda el ACK al nodo coordinador
- CL=QUORUM:  alcanza con que dos de los nodos replica respondan el ACK al nodo coordinador
- CL=ALL:  TODOS los nodos replica respondan el ACK al nodo coordinador

Este aumento de consistencia tiene su contraparte en que aumenta la latencia, debido a que se debe esperar que aumente la cantidad de nodos que responden

##### Immediate Consistency

- CL(read) + CL(write) > RF
- CL(read)[QUORUM] + CL(write)[QUORUM] ==> Estandar


##### Weak(er) Consistency/ Eventual consistency
- CL(read)[ONE] + CL(write)[ONE] ==> Estandar

