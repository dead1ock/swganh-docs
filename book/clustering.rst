Clustering
==========
MMOs require alot of processing power, sometimes more then one physical processing unit can provide. In these situations,
clustering is employed to split up tasks between two or more physical machines. This creates a new set of complexities however; Messages must be exchanged between these services and resources must be properly located.

Clustering is only recommended for server administrators faced with high server populations (4 digit number). The goal is to take the most resource intensive tasks and split them off from the main simulation to allow for scaling.

Service Schemas
###############
SWG:ANH employs a very simple clustering schema. A Service Schema is a collection of Services which run together on a single executable. There are 3 main Service Schemas that make up a cluster:

Login
-----
* Scale: 1 per-Cluster
One Login Service Schema is required per-cluster, but one can span between multiple galaxies. Its single task is to authenticate users and forward them to the correct Connection Service.

Connection
----------
* Scale: 1+ per-Cluster
The sole purpous a Connection service is to process incoming messages from clients (after login), convert it to simulation data and route it to the correct service. Although that may seem like a small list of tasks, these tasks make up the majority of the intensive processing that is required.

Simulation
----------
* Scale: 1-per Cluster
This is where "the game" is actually ran. All the services which affect gameplay reside in this Service Schema.

Configuring
###########
By default, the server is configured to start all Service Schemas on a single executable.