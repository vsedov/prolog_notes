  title: index
  description:
  authors: viv
  categories:
  created: 2022-03-04
  version: 0.0.11

# Chapter 2 Uniformed Search
## Examples of Uniformed Search
Uniformed search is a tree search, or the concept of how one would iterate through a given tree

1. Breadth First Search
2. Depth First Search
3. Depth Limited Search
4. Iterative Deepening Search _Sounds cool right_

## Tree search Algorithm

### Basic Information
State vs Nodes

1. A _**State**_ is a representation of a some physicial figure.

2. A _**Node**_ is a structure [Data Structure] Containing a search tree of the following types
    - Parent
    - Child
    - Depth [ Height ]
    - Path Cost -> g(n)

      3. A _**State**_ Does not have Parent, child, depth or path cost !!

```comment

     ┌──   ──┐     <- State                               ┌──────┐
     │ 5 4 _ ├────────────── <-   ┌─┬────────────────────►│Parent│ Node
     │ 6 1 8 │                    │A│ Node                └──────┘
     │ 7 3 2 │             ┌─────►└─┘◄─────┐
     └──   ──┘             │               │
                           │               │
                         ┌─┤               ├─┐
                         │N│               │N│ -- Children Node
                         └─┘               └─┘
```
From a tree perspective, a set can be represented in a matrix, where you have multiple Nodes - that has a parent
We call that parent through some action

Take that matrix above - where if your initial Node was to go left from node % the path cost would be 4

#### How do you create this ?
Implemention needs one to create a _Expand_ Function, that creates new nodes filling various fields and ussing a SuccesorFn of the problem to create
the corresponding states -> Easily done in prolog

### The algorithm
```python
  def TreeSearch(Problem, Statergy) -> solution or failure:
    # -- Initalise search with problem as the root node
    x = RootNode
    front = list() # Some sort of list - datastructure

    While True:
      if tree[0] is None:
          return False
      # choose and remove a lead node L from the front {depends on stratergy}
      L = front.remove("Depends on stratergy")
      if L is in Goal_State :
        return solution
      else:
        x = expand(L)
        front.append(x)
        # Expand L and adding it to the resulting nodes to the frntier
```

#### Whats going on here

This algorithm listed above is the base algorithm between all the searches that are listed above
1. DFS
2. BFS
3. Depth Deepning Search
4. Iterative Deepening Search

- Initalise a search tree with an initial state - So for example when you are passing a root node

- The front list will contain the other list nodes avaliable at any given time, for expansion for any given time.
    - Meaning this can be used to expand the search tree

- If you dont have any nodes within the front list, that would mean that you have explored all the possible
  nodes within that given datastructure

1. If the front of the tree is empty then we return fail: we already searched the search tree
2. Remove a lead node L, depending on the search strat, could be fifo , lifo, and it could be based on the cost
3. Once the node is retreved, we can check if it is a goal
4. If it is not, then we have to expand the goal, and then we have to expand and generate new nodes
```comment
                                        ┌─────┐
    ┌───────────────────────────────►   │ Arad│    ┌──────────────────┐
    │                ┌────┬─────────┬───┴──┬──┴────┼───────────┐      │
    │                │    │  ┌──────┼──────┼───────┼────┐      │      │
    │                │    │  │      │      │       │    │      │      │
    │                │    │  ▼      │      ▼       │    ▼      │      │
    │                │    │ Sibu    │     Tisma    │    Zac    │      │
    │                └──┬─┴──┼──────┼──────────────┼┬────┼─────┴──────┤
    │ ┌──┬──────────────┴────┼┐     │              ││  ┌─┴─────┐      │
    │ │  │ ┌────┬───┬────┬───┘│     │              ││  │       │      │
    │ │  │ │    │   │    │    │     │              ││  │       │      │
    │ │  │ ▼    ▼   ▼    ▼    │     │              ││  ▼       ▼      │
    └─┼──┤arad  bob ola  foo  │     │              ││  Bill   Desmond │
      └──┴────────────────────┴─────┘              │└─────────────────┤
```
└──────────────────┘
Trees have their own recursive call, we are checking if we are reaching / hit a node at a given point
We do this through evaluating some tree statergy at a given point,

**Note**
- We have to have a list that checks if we have gone through a given node, whats important here is that we
  check if the node is visited or not so we can continue and ignore that given child, as you woudl end up having a forever loop.
  Which is not ideal .

> Example tree Listed above ^ The question now is how do you traverse this given tree?

1. For example if we Have the initial state, Arand, we first expand the search tree
2. From expanding we get [](Sibu,%20Trisma,%20Zac)
        - Sibu
          Expand Sibu :
    - Arand
    - Bob
    - Ola
    - Foo
        - Tisma
    - Nothing
        - Zac
    - Bill
    - Desmond

This expansion is recursive, what it does is adds teh set of new nodes into our list when we are exploring a given tree

_Expanding allows us to generate Child Nodes_
- We check if that node is already in that given list or not : if it is and we have searched everything from that Child, we can move to the next value
- Ideally that is what that algorithm does . The basis for it is having some front list that checks if the
  values are within it or not, and if it is stop and move on .

you can have the same value twice hence why we check
# Different Types of uniformed searches
1. Breadth first
2. Depth First
3. Depth Limited Search
4. Iterative Deepening search

- Each search has their own properteries, refer to the book if you want further details
## Breadth First Search
1. You go through each Level
  2. you bassicly go from left to right, when doing a breadth first search

Breadth first search is an algorithm for traversing or searching a whole tree, it starts at the root node or something problem node, and will explore the neighbours of the nodes first before moving to the next leve neighbours.

_**It uses a FIFO Queue**_

## Depth First Search
You start fro the root, at teh very root and explore to the depth, such that you would explore as far down as possible - along each branch before you backtrack towards the next possible item

There are different types of backtracking methods that would lead to a more optimal method to use ds

## Depth Limited Search
Depthj limited search is almost equal to DFS, but because DFS has this unlimited depth factore, such that you could have a infinite state space and that you problem is no longer bound, the depth limited search negates that issue; as in what it does from the given point is limited the depth amount - it is predetermined and very limiting .

## Uniform - Cost Searc
Uniform Cost search is a tree search algo, related to the breadth first search where bfs determines a path that has the least number of edges, or that the total cost is reduced, and would work through that instead.  the uniform cost search determines a path to the goal state that has the lowest weight / bias

One of the biggest disadvantages is there can be multiple long paths so uniform cost has to explore each and every one of them .

## Iterative Deepening Search
Iterative deepening search is an epic name

What this does is abuses the depth limited search where we have a depth limit but as soon as we know that there is no solution in some given depth we increase the depth and do a depth limited search on there to ensure that something is there, in short we are iterating over the dpeth limit and increaseing it till something is found .

# Summary
## Info
### State info
- State: It provides all the information about the environment.

- Goal State: The desired resulting condition in a given problem and the kind of search algorithm we are looking for.

- Goal Test: The test to determine whether a particular state is a goal state.

- Path/Step Cost: These are integers that represent the cost to move from one node to another node.

- Space Complexity: A function describing the amount of space(memory) an algorithm takes in terms of input to the algorithm.

- Time Complexity: A function describing the amount of time the algorithm takes in terms of input to the algorithm.

- Optimal: Extent of preference of the algorithm

### Tree info
- ‘b‘ – maximum branching factor in a tree.

- ‘d‘ – the depth of the least-cost solution.

- ‘m‘ – maximum depth state space(maybe infinity)

## Breadth First Search
[Search]("https://www.analyticsvidhya.com/blog/2021/02/uninformed-search-algorithms-in-ai/")
Follows a lexographical order :
### Complete
Yes if B is FINITE
### Time
Big O of B power d
$$
O(bᵈ)
b¹ + b² + b³ + ... bᵈ = O(bᵈ)
d is out total depth - every depth we go we have to increase our value as shown above
$$
remember
d = depth of the solution
b = number of branches of tree i.e maximum branching factor in a tree
Meaning your Big would be

your maximum branching factor to the power of the depth of your solution

### Space
$$
O(bᵈ)
$$

### Optimal ?
Yes if every step cost is the exact same.
You can say the following
```python
  if all(step) == ConstantValue:
    return True
  return False
```

i.e if the step cost is a constant

## Uniform Cost
The cooler BFS as i like say
### Complete
It is complete under the condition that the number of branches for the tree are at step zero
such that everything is traversed, otherwise this would not be Complete
Look at the examples within your book.

### Time
$$
  O(b^{ᶜ⁄ᴱ)
$$
where E is the lowest cost such that, C is the optimal Cost

every layer we go, we have to increase that by what ever the most optimal and current cost would be
What we eval to is around

```
  O(B^(d+1))
```
E is the cost of each single step - when you add everything back together, is similar to breadthfirst search -> B number of branches have been explored and the depth is most optimal solution that is being explored.

### Space
$$
  O(b^{ᶜ⁄ᴱ)
$$
Space and time complexity would be the same as you are travesing a tree in the same method and storing / poping the same way, such that it has a low space complexity compartivly to BFS

### Optimal ?
Depends on what you are dealing with, very dependent on the problem type :
most cases this would be more optimal.

Even if the cost is not optimal it is better than a depth first search, due to the cost factor being so low

## Depth First Search

### Complete
No, DFS is not complete - it fails in infinite depth spaces, spaces with loops : then you will have a recursive loop, and a continuation of all the values

It is complete under the condition that the _space_ is **finite**

### Time
O(b^m)
Big O of all the branches covered to the power of the maximum depth state [](%20big%20issue%20with%20the%20max%20depth%20state%20)
If the depth space is infnite then you will keep going and have a memory issue : under the condition that the spce is Finite then you Big o is to go all the values from the lowest LHS to the lowest RHS

For every layer that have b number of nodes, we check through each of that given node
B number of nodes and we split that between b/2 -> M number total depth
### Space
Linear space -> O(bm)
B number of child nodes for each level, and choose one of them to go to the maximum depth of the nodes
```comment
        │
        │
      ┌─┘──┐
      │    ▼
    ┌─┴┐
   ┌┘  ▼
   ▼ -> Max branch we would go to, and b number of nodes will be searched - and remembered through the process
   M is more larger than d -> time complexity will be worse but under the process, we only need to remember singlular banches => Search space is then reduced
i.e the total number of steps that is required is reduced.
```

### Optimal ?
If you do not have a finite space then no this would no be optimal, as you entire answer can be on another layer - i.e what if you are searching an infinite RHS and the answer is on the LHS ?
Going to be hard to represent that

Optimal under the condition that it is finite.

## Depth Limited Search
DLS -> You have a predetermined depth limit
DLS  tends to have a cutoff limit -> when a failure would occour
### Complete
No it is note complete
### Time
$$
Time Complexity: O(b^l)  where, l -> depth-limit
$$
And that your given state is finite
depth limited search would require the following

- Depth limit Recall
- l value would have to be preterderminted - due to this, information can be lost or items can not be
  found.

### Space
```math
Space complexity: O(bl)
```
One of the most memory effiient algorithms, where you search in a dfs mannor through a list using a limited depth,
very intriguring and has a rather interesting limit val - we can call this effcient on the condition teh goal node is < l th node
otherwise its not complete as stated above

Linear time with respect of what ever our depth limited or limited value for our depth would be.
### Optimal ?
Only if your power _i_ value is to the same as your depth limit value d

## Iterative Deepening Search
Make sure you account for step size

### Complete
Yes this is complete, as we go through all nodes till we find our values
we say this is complete by

$Complet$
It is complete through depth limiting
_

### Time
The iterative deepening search is based on b to the power d

### Space
bd -> optimal due to the fact we find out value through teh ammount of branches and the lowest depth to where teh value may be
in some sense we combine both BFS and DFS in one.
### Optimal ?
Yes -> IFF the step size are the same, or you have miinimal step size to work with

## Bidirectional Breadth First Search
--Wasnt covered that much for some reason--
Foward Search : looking in from of the end from the start
Backward search: looking from end to the star backwards
### Complete
Yes
### Time
O(B^[](d/2))
### Space
O(B^[](d/2))
### Optimal ?
Yes if you have a uniform searc