# The  mathematical formulation of LRP

***The problem description***

​	Let an undirected graph $G=(V,E),V = I∪J$ ,where  I={0,1,2,...,m-1}​, is the set of potential depots,total number is m;J={0,1,2,...,n-1},is the set of customers,total number is n;K={0,1,2,...,k-1},is the set of  the identical vehicles,the number of available vehicle is infinite,here we set the number of vehicle equals k which overweight the number needed.$E =( I∪J)×J,c(i,j)$ is the cost of edge $(i,j)(i,j∈V)$,and $c(i,j)=c(j,i)$.here the cost means the Euclidean distance between node i with node j;we associate capacities $q(i)$ and installation cost $f(i), \forall  i ∈ I$, and demands $d(j) ,\forall  j ∈ J$ and the vehicle capacity Q and the utilization cost C,$\forall  v∈K$;

​	In our problem, a route is an elementary cycle in G containing exactly one depot in I and a subset of the customers J. Therefore, a feasible solution to LRP is a set of routes such that:(i) each customer belongs to exactly one route ; (ii) the sum of the customers’ demands in a route does not exceed Q, the vehicle capacity ;  (iii) the sum of the customers’ demands in all routes associated with depot i ∈ I does not exceed q(i). Then, the objective is to find a feasible solution such that the route cost, given by the sum of the costs of the edges in each route, and the installation costs of depots used in the solution and the cost of the vehicle used, are minimized.

***Known***

$I$:the set of potential depots

$J$:the set of customers

$V​$: the set of vehicles

$c(i,j)$:the cost of edge(i,j)

$q(i)$: the  capacity of  depot i

$f(i)​$:the open cost of  depot i

$d(j)​$:the demand of customer j

$Q$:the capacity of vehicle

$C$:the  utilization cost of vehicle

##### Decision variable*

$$
y(i)=\begin{cases} 1,depot \quad i\quad is\quad open\\ 0, otherwise\end{cases}\quad\forall i∈I
$$

$$
x_{ij}^v=\begin{cases} 1,if \quad edge(i,j)\quad is\quad traversed\quad by\quad vehicle\quad v\\ 0,otherwise\end{cases}\forall i,j∈I∪J,i\neq j,v∈V\\
note:edge(i,j)\quad means\quad from\quad node\quad i\quad to \quad node \quad j
$$

$$
f(i,j)=\begin{cases} 1,customer \quad j\quad is\quad served\quad by\quad depot\quad i\quad or\quad j∈I \\ 0,otherwise\end{cases}\quad\forall i∈I,j∈J
$$

$$
z(i,v)=\begin{cases} 1,vehicle \quad v\quad  serve\quad depot\quad i \\ 0,otherwise\end{cases}\quad\forall i∈I,v∈V
$$



****

**Objective function***
$$
min\quad tot\_cost= \sum_{i∈I}{y(i)f(i)}+\sum_{i∈I∪J}\sum_{j∈I∪J,i\neq j}\sum_{v∈K}{x_{ij}^vc(i,j)}+\sum_{i∈I}\sum_{v∈V}{Cz(i,v)}
$$
***Constrains***

a customer j must be served by one depot
$$
\sum_{i∈I}f(i,j)=1,\forall j∈J
$$
only  when one vehicle used by depot i  visit the customer j
$$
z(i,v) +\sum_{i1∈I∪J,i1\neq j}x_{i1,j}^v \le f(i,j)+1 \quad \forall i∈I,j∈J,v∈V
$$

$$
\sum_{i1∈I∪J,i1\neq j}x_{i1,j}^v+ f(i,j) \le z(i,v)+1\quad \forall i∈I,j∈J,v∈V
$$


//a vehicle must start and end at the same position
$$
\sum_{j∈I∪J,i\neq j}x_{ij}^v=\sum_{j∈I∪J,i\neq j}x_{ji}^v\quad \forall i∈I∪J,v∈K
$$
a vehicle only serve one depot at most
$$
\sum_{i∈I}z(i,v) \le 1 \quad \forall v∈K
$$
//subtour constrain
$$
\sum_{i∈S}\sum_{j∈S,i \neq j}x_{ij}^v \le |S|-1  \quad \forall S\subset J， v∈K
$$
也可写成
$$
\sum_{j∈J}x_{ij}^v = z(i,v)\quad \forall i∈I,v∈V  
$$
each customer must be visited only once and only by one used vehicle
$$
\sum_{v∈K}\sum_{i∈I\cup J,i \neq j}{x_{ij}^v} =1\quad \forall j∈J
$$

the total demands in one route shouldn't exceed one vehicle's capacity
$$
\sum_{i∈I∪J}\sum_{j∈J,i\neq j}{x_{ij}^vd_j} \leq Q\quad \forall v∈K
$$
the total demands in one depot's all routes shouldn't exceed the depot's capacity

$$
\sum_{j∈J}{f(i,j)d_j} \le q(i)\quad\forall i∈I
$$

vehicle serve the open depot
$$
z(i,v)\le y(i)\quad\forall i∈I
$$
