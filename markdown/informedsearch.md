  title: index
  description:
  authors: viv
  categories:
  created: 2022-03-06
  version: 0.0.11

# Informed Search
## What is informed search ?
- Problem specific - informed search, used in problem specific

You use informed search when you have extra information of the situation/ problem situation

## Best First Search
- Dont get confused with Breadth First Search, as easy as it is to get confused

Best First Search is an instance of the tree algorithm, it has this amazing loop checking and a way to define the order
of when or how a node would expand

```python
def tree_search(problem, strat)->bool:
  x  = list()
  x.insert(0, problem)
  # Initalise the search tree with a state and let problem be its root

  while True:
    if len(x) == 0:
      return False

    L = x.pop() # wdepends on how you pop it, but you can base it of a functional value

    if L in goal_state :
      return L
    else :

      if L not in explored_set:
        if expand(L).child not in explored_set
          x.append(expand(L).child_nodes)
        explored_set.append(L)
```

Very simple psuedo python code, to represent how the loop check does, we hhave two lists to call from, the explored list set that contains all the nodes that we have explored
and the frontier list set that is teh list that we are adding to , i.e the expanded nodes

1. Tree structure is required
2. Initial state is required
3. Set the frontier
4. For exapme if the frontier of the search tree is empty that woudl mean that we have visited all teh nodes - else we choose and remove a node
5. i.e how woudl you remove a node, lifo fifo, it depends on a situation, or you can base it off a cost function

### Idea Behind best first search

1. Use a $evaluate$ function f(n) which is a cost estimate
- you have a list of all the paths and then you would also have an estimate of those paths to a goal, based on
  teh evaluate function
```python
[(1,50), (3,30) ... ]
```
  Think of a List(Tuple(Path, Evaluation))

2. Sorted by the cost of the nodes that you are expanding
3. Frontier is a queue - sorted in decreasing order, with respect of the values that you want to get

#### Special Cases
1. Greedy search
Cost estimate(node) = heuristic function to goal(node)

i.e f(n) = h(n)
heuristic function to estimatated cost from current goal to node.

2. A* Search
Cost estimate(node) = actual cost(node) + heuristic function to goal(node).
i.e f(n) = g(n) + h(n)

## Heuristic function
Best First search can go with multiple search options
One of them is the heuristic function h(n)

1. _h(n)_ is the estimated cost of the cheapeast path from teh state at node N to the goal state

2. Unlike g(n) it depends on teh state node n ;

3. Provides information on top of the problem description so it informs the search, in this case you are constantly updating your search algorithm to find the most optimal solution
This prediction comes in handy when trying to define some value
- Estimated information - will normally be provided as additinal information to a given solution

- Sasy you are trying to go from location A to location B :- Think of what information you have at the time, and
  what additional information you would require to solve this problem ?
  Current Information
- General location of A and B
- Cords
- Cost
  Additional Information -> Not always provided but we require extra knoledge
- Total distance
- external routes
  etc ...

4. You are _not_ allowed to have non negative values implies h(n)> 0
The only time a heuristic search can equal 0, or the only time where _h(n) = 0_ is when _h(n) = 0 if n is in goals_

## Greedy search
Greedy search expands the node that appears to be teh closest to the goal .

- The idea is that it will lead us closer to the goal state
- Just use the ehuristic function
$$
f(n) = h(n)
$$
- you expand the node with teh least cost within the frontier list

### Main Information About Greedy Search
You have different types of Best First Search Algorithms, with very similar complexity, there are a few things that make it unique.

Greedy search is gredy, it is completly based on the fact that it needs some sort of heursitcal value to work of, it does not deal with your current weights.

As mentioned above it requries that :
$$
f(n) = h(n)
$$
What this means is that the herusitc value of our search is going to be our call value, or our search weight for what node to go next.
Heuristics follow a few goals

### Goals
1. H(n) is the estimated and the _CHEAPEST_ point from some x to y state
2. unlike g(n) it depends on the state of node n - > external factors are applied to this
3. heursitics deal with external info

Back to greedy now
```comment

            4  ??? 10
        B  ???????????????????????? A
           ???      ???
           ???      ???
           ???      ???
           21     20
           ???       ???
           ???????????????????????????
               50
```
In this case a greedy algo would just pick B over A, due to the fact that the end node to get to 20 would be way more expensive, when it could fo just went from A

The principle of greedy has allot of rng, and allot of recursive, and looping issues as well

#### Is it complete ?
No - it is not complete as you can have loops, which ideally you do not want.

#### Time and space  ?
$Time$
O(B^m)
_Similar to Big O of Depth First Search
Cost - is the same, due to the fact we are exploring a depth, and expanding that, we are not going from edge to edge, we are following a pure depth down search on some cheap node

$Space$
O(B^m)
_Similar to Big O of depth First Search

## A * Search
To first point out this search is overpowered, it can do allot, if you have the right information for it
Most cases you can do an A* Search with Dynamic programming, which is pretty cool as well, it goes brrr

--Information--

### Important part and Some code to justify it
The most important part of A* is that it seperates it self from other traveral types - and that it has a based decision on the given information that you give it, its kinda cool when you look at it change with different information, it follows a Ai logical approach as i like to say

```python
def aStarAlgo(start_node, stop_node):

        open_set = set(start_node)
        closed_set = set()
        g = {} #store distance from starting node
        parents = {}# parents contains an adjacency map of all nodes

        #ditance of starting node from itself is zero
        g[start_node] = 0
        #start_node is root node i.e it has no parent nodes
        #so start_node is set to its own parent node
        parents[start_node] = start_node

        while len(open_set) > 0:
            n = None

            #node with lowest f() is found
            for v in open_set:
                if n == None or g[v] + heuristic(v) < g[n] + heuristic(n):
                    n = v

            if n == stop_node or Graph_nodes[n] == None:
                pass
            else:
                for (m, weight) in get_neighbors(n):
                    #nodes 'm' not in first and last set are added to first
                    #n is set its parent
                    if m not in open_set and m not in closed_set:
                        open_set.add(m)
                        parents[m] = n
                        g[m] = g[n] + weight

                    #for each node m,compare its distance from start i.e g(m) to the
                    #from start through n node
                    else:
                        if g[m] > g[n] + weight:
                            #update g(m)
                            g[m] = g[n] + weight
                            #change parent of m to n
                            parents[m] = n

                            #if m in closed set,remove and add to open
                            if m in closed_set:
                                closed_set.remove(m)
                                open_set.add(m)

            if n == None:
                print('Path does not exist!')
                return None

            # if the current node is the stop_node
            # then we begin reconstructin the path from it to the start_node
            if n == stop_node:
                path = []

                while parents[n] != n:
                    path.append(n)
                    n = parents[n]

                path.append(start_node)

                path.reverse()

                print('Path found: {}'.format(path))
                return path

            # remove n from the open_list, and add it to closed_list
            # because all of his neighbors were inspected
            open_set.remove(n)
            closed_set.add(n)

        print('Path does not exist!')
        return None

#define fuction to return neighbor and its distance
#from the passed node
def get_neighbors(v):
    if v in Graph_nodes:
        return Graph_nodes[v]
    else:
        return None
#for simplicity we ll consider heuristic distances given
#and this function returns heuristic distance for all nodes
def heuristic(n):
        H_dist = {
            'A': 11,
            'B': 6,
            'C': 99,
            'D': 1,
            'E': 7,
            'G': 0,

        }

        return H_dist[n]

#Describe your graph here
Graph_nodes = {
    'A': [('B', 2), ('E', 3)],
    'B': [('C', 1),('G', 9)],
    'C': None,
    'E': [('D', 6)],
    'D': [('G', 1)],

}
aStarAlgo('A', 'G')
```

### Conditions for A*
#### Basic Idea
- A* is based on heuristic methods, to help achieve its optimal value.
- If
$$
  fn(n) -> cost
$$

then A* ensure that it chooses the lowest cost, with respect of its heuristically factor
The full calculation of the cost given of each node is shown below

$$
f(n)=g(n)+h(n)f(n)=g(n)+h(n)

g(n) = shows the shortest path???s value from the starting node to node n
h(n) = The heuristic approximation of the value of the node
$$

#### Heuristics
##### Properties what is it ? etc
A herustical factor, is a function that helps the rank , in some sense it gives an alternative seartch pattern that an algorithm can work on, more so its an estimate, the major thing about this is this is extra information, on top of what the graph current contains

A heuristic as it is simply called, a heuristic function that helps rank the alternatives given in a search algorithm at each of its steps. It can either produce a result on its own or work in conjugation with a given algorithm to create a result. Essentially, a heuristic function helps algorithms to make the best decision faster and more efficiently. This ranking is made based on the best available information and helps the algorithm to decide on the best possible branch to follow. Admissibility and consistency are the two fundamental properties of a heuristic function.

##### Admissibility of the heuristic function
A* will fail, if  the herusitcs that are given are not admissable,

_What does that mean ?_
Well, Admisable implies that you cannot have a herusitcal value that is over estimated, which means that you cannot over estrimate a herusitc, but on the other hand you can under estimate it, which is actually good.

Think about

$$
Since G(n) is the actual cost, if h(n) is admissible then f(n) never overestimates the true cost
$$

but on the other hand if it is not admissable, then you overestimate the cost and you have large implications to that

$$
f(n) = g(n) + h(n)
since g(n) is the actual cost, if h(n) is admissable, you have the options between

A. Underestimate
B. Correct estimate
$$
Admissible is great because you can say that something can be on point or we can underestimate and say ah it might be a bit cheaper when in reality it is expensive .

###### Colonary for admissibility
if h(n) is overestimated then if the algo reaches the goal node, by some path, the principle is that we could of missed a node, say we have out best case path
$$
Call best case path (A) then if our current path
C(Path) < f(A)
$$
we know there was an overestimate
Because h(n) is seemingly worse than an already seen path, and in that case it wont even bother looking at that path, talk about it being big brain, cant even look for shortest path without help, STUPID HMPH

###### what happens if its not admissable
**You die**

1. You miss paths you could of went to
2. Kinda replicate what greedy does, which is not what this algo should do

If on the other hand it is admissible, then we can say its >= of what we already have, in that case thats good, we want that, because that means we wont miss any paths, when something is not admisslbe, it would mean tht we have missed multiple paths, the lowest given path is a given for a fact if it is admissable,
#### Consistent
A heuristic function is consistent if the estimate of a given heuristic function turns out to be equal to, or less than the distance between the goal (n) and a neighbour, and the cost calculated to reach that neighbour.

The efficiency of an A* algorithm highly depends on the quality of its heuristic function. Wonder why this algorithm is preferred and used in many software systems? There is no single facet of AI where A*algorithm has not found its application. From search optimization to games, robotics and machine learning, A* algorithm is an inevitable part of a smart program.

### Properties

#### Complete
Yes A* is indeed complete, under the condition
$$
f <= f(G)
$$

#### Time
Exponential time (relative to error in the following)
$$
relative error -> h x length of solution
- meaning that the error or time rate, is expanded with each programmatic node search
-> it runs in exponential time
$$

#### Space
Well you store everything in memory, i.e all your nodes, so you end up keeping all your explored and non explored in memory
good way about this is doing a matrix store

#### Optimal ?
well yes and no, it is optimal with respect that it cannot explore f_i+1 unless f_i is explored fully, think of how depth first would work in that situation
but at the same time it is not optimal due to how long the time constraints take

$$
Let C* be the cost of all the optimal solutions

- A* expands all nodes with f(n)  < C*
- A* expands some nodes with f(n) = C*
- A* expands no nodes that are f(n) > c
$$

**Important**
- A* expands all nodes with f(n)  < C*
- A* expands some nodes with f(n) = C*
- A* expands no nodes that are f(n) > c

## Overall Properties between Greedy and A*

$with or without loopChecking$
basis is that our values can have a loop check where we dont go in a infinite loop
_

### A* Properties [](No%20loop)
#### Complete
Yes under the condition that our set or values _b_ is finite, and that our initial step cost
is over o

$$
b > 0
len(b) is some finite value
$$

#### Optimal
Yes under the condition that H holds admissible Properties, else its just pointless

### A* Properties [](With%20loop)
#### Complete
Yes, this is teh same with or without loop.
#### Optimal
Yes but the good thing about this is that you dont need admissibility but you need to have consitency
if H is not consistent, then it Fails

### Greedy [](No%20loop)
#### Complete
Yes under the condtioon that you have a admisable map
#### Optimal
not really

### Greedy [](with%20loop)
#### Complete
well no Cause you can go in a infnite loop strand

#### Optimal
Not really

## A* A bit more in detail, and common FAQs
A star is not just that. there is more.

With the current a * our time complexity is way too high, which is not optimal, there are ways to improve this factor.

A* allows us to expand nodes in order of increasing value of f
What this means is adding f-countours of nodes, something similar to breadth first add layers
we can then have f = f_i where f_i <= f_i+1