  title: extended_informed_search
  description:
  authors: viv
  categories:
  created: 2022-04-16
  version: 0.0.11

# Search Problem
- states within the the world, or parts that are within the world
- Actions and costs - encoded within our succesor function, what happens when we you go  to the next state
- Successor function, and world functions
- Start state and goal test
## Search tree
- Nodes : represent plans of reaching states
- Planes have costs with each action,
## Search algorithm
- Something that builds this search tree
- DFS, BFS , IDFS , Depth limited and uniform
    - How they paradise from how they pick out data from the fringe [ frontier list ]
- Optimal finds the least cost plan -> Guaranteed to find the least cost
```
function tree_search [ problem , state]
  get search tree and initial state
  loop do
    if there are no values for expansion and then
        return fail
        else if the node contains the goal state then return the corresponding solution
      else:
          keep expanding the node and keep going till you find the right values
```
  Tree search >:
  DFS and BFS are pretty much the same, depends on the right strat, to get everything to return all the values, which would eval all your strats .

# Heuristic
a Rule of thumb : a function is something you do, something you do to follow a given rule
A function that maps a state to real memembers

It is something that will tell you about the state or tell you how close you are towards the given goal

Main thing is that you have to make them designed for each design problem . It would then define how clever the problem is : each problem has its own heuristic that it would have to work wit .

- Far away from the goal = high score high cost

- Close to the goal = low score low cost

    - Heuristics are a point of estimate : they give us a guide on where we have to go to some place

## Greedy
- Tree Search
  Guided by heuristic

- You build the search tree but only from the heuristic value, nothing else
- Greedy is a way to select what node to expand first : so you state what heuristic value would be
    - and that would be the next thing that you would expand

- Main issue is that you can get a huge loop, or circular motion with this

1. Greedy does not account for the traversal that has already occurred .
2. You merely look ahead, you do not look at what you went through

   Greedy search is like depth first search, you keep moving down the deeper tree, but you would have to go through the entire tree if it would have to .

- it would go deep to where it thinks where the goal would be
- you have to makes use that the heuristics are valid and sound
- Worst case likely badly guided depth first search

## A star
Is a combination of uniform cost search and greedy cost search, thing is to note it knows what is the cheapest point to go by: its a pretty cools search.

Think of the turtle and the rabbit: think back to how that works

Combining UCS and Greedy together:
[img/2022-04-16-21-53-14.png](name)




- Uniform cost orders by path cost, or backwards cost g(n)
- Greedy orders by goal procimity or forward cost h(n)

_Now lets be big brain and combine them_.
