# The  mathematical formulation of LRP

***The problem description***

​	Let an undirected graph G=(V,E),V = I∪J ,where  I={0,1,2,...,m-1}, is the set of potential depots,total number is m;J={0,1,2,...,n-1},is the set of customers,total number is n;K={0,1,2,...,k},is the set of  the identical Vehicles,the number of available vehicle is infinite,here we set the number of vehicle equals k which overweight the number needed.E = E1∪E2,where E1=I×J and E2=J×J;c(i,j) is the cost of edge (i,j)(i,j∈V),here the cost means the Euclidean distance between node i with node j;we associate capacities q(i) and installation cost f(i), for i ∈ I, and demands d(j) for j ∈ J and the vehicle capacity Q and the utilization cost C,for v∈K;In our problem, a route is an elementary cycle in G containing exactly one depot in I and a subset of the customers J. Therefore, a feasible solution to LRP is a set of routes such that:(i) each customer belongs to exactly one route ; (ii) the sum of the customers’ demands in a route does not exceed Q, the vehicle capacity ;  (iii) the sum of the customers’ demands in all routes associated with depot i ∈ I does not exceed q(i). Then, the objective is to find a feasible solution such that the route cost, given by the sum of the costs of the edges in each route, and the installation costs of depots used in the solution and the cost of the vehicle used, are minimized.

***Known***

I:the set of potential depots

J:the set of customers

K: the set of vehicles

E:the Euclidean distance/cost between node i and node j, for i∈I,j∈I∪J

q(i): the  capacity of  depot i

f(i):the open cost of  depot i

d(j):the demand of customer j

Q:the capacity of vehicle

C:the  utilization cost of vehicle

##### Decision variable*

$$
y(i)=\begin{cases} 1,depot \quad i\quad is\quad open\\ 0, otherwise\end{cases}\quad\forall i∈I\quad(1)
$$

$$
f(i,j)=\begin{cases} 1,customer \quad j\quad is\quad served\quad by\quad depot\quad i\\ 0,otherwise\end{cases}\quad\forall i∈I,j∈J\quad(2)
$$

$$
x_{ij}^v=\begin{cases} 1,if \quad node j\quad is\quad traversed\quad by\quad vehicle\quad v\\ 0,otherwise\end{cases}\forall i∈V,j∈J,v∈K(3)
$$

$$
z(v)=\begin{cases} 1,if\quad vehicle\quad v\quad is\quad used\\0,otherwise\end{cases}\quad\forall v∈K\quad(4)
$$

***Objective function***
$$
min\quad tot\_cost= \sum_{i∈I}{y(i)f(i)}+\sum_{i∈V}\sum_{j∈V}\sum_{v∈K}{x_{ij}^vc(i,j)}+\sum_{v∈K}{Cz(v)}\quad(5)
$$
***Constrains***

a customer must be served by one open depot and only can be served by one open depot 
$$
\sum_{i∈I}{f(i,j)}=1\quad \forall j∈J\quad (6)
$$
a vehicle only can be used by one open depot //a vehicle must start and end at the same depot
$$
\sum_{i∈I}(\sum_{j∈J}x_{ij}^v+\sum_{j∈J}x_{ji}^v)=2z(v)\quad \forall v∈K\quad (7).
$$
each edge  can be traversed only once and only by one used vehicle at most/each customer must be visited only once and only by one used vehicle
$$
\sum_{i∈V}\sum_{v∈K}{x_{ij}^v} = 1\quad \forall j∈J\quad (8)
$$

the total demands in one route shouldn't exceed one vehicle's capacity
$$
\sum_{i∈V}\sum_{j∈J}{x_{ij}^vd_j} \leq Q\quad \forall v∈K\quad (9)
$$
the total demands in one depot's all routes shouldn't exceed the depot's capacity

$$
\sum_{i∈I}\sum_{j∈J}{f(i,j)d_j} \leq q(i)\quad (10)
$$

only the open depot can use vehicle
$$
\sum_{j∈J}{x_{i,j}^v} \leq y(i)k\quad \forall i∈I\quad (11)
$$
only the used vehicle can service customer
$$
x_{i,j}^v \leq z(v)\quad \forall i,j∈V,v∈K\quad (12)
$$
a route only include one depot
$$
\sum_{i∈I}\sum_{j∈J}{x_{i,j}^v} = \sum_{i∈I}\sum_{j∈J}{x_{j,i}^v} = 1\quad (13)
$$
no edge between depot and depot
$$
\sum_{i∈I}\sum_{j∈I}\sum_{v∈K}{x_{i,j}^v} = 0\quad (14)
$$
