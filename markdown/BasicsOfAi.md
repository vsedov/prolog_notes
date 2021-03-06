  title: index
  description:
  authors: viv
  categories:
  created: 2022-03-03
  version: 0.0.11

# Developers Note
1. Main Focus is Single State problems

# Chapter 1 : Introduction  [](Lecture_1)

## Why do we need search
A     B
┌─────┐
├┬─┐  │
││ │  │
└┴─┴──┘C
D E  F

- Consider each letter a node and a path
- Each path has some sort of weighiting that allows us to go through and caculate the following items

- [x] Shortest Path
- [x] Quickest Path
- [x] Least Expensive Path

We use this as a measure of how good out algorithm is presenting some given search over a period of time

- What does this mean ?

Most cases In _AI_ We rely on teh factor of searching a given value, or a set of given values where we have a start node
and where we want to get to, at the very end, what is the main goal to be aiming for.

We use graphs and trees to allow us to search in a certain way to provide and give that information.

### Why ?
- We want to convert a real world problem into a computational perspective - such that their are weightings bias etc , to uphold for changes.
- Different search algorithms are used , to allow us to search and find the most optimal path to a given node.

_Book_
```comment
Look at Notebook for diagram iliustrations on the Vaccume work { Need notes on the given diagram }
```

### Example Diagram
a  b  c
┌──       ──┐
a │  7  2  4  │   - Examples like this, require a informed search
b │  5  _  6  │
c │  8  3  1  │
└──       ──┘
What this tells us is that say we have some start state, consider 7, where the node from a to a is 7
we can make a table to describe the best and most optimal way of getting to the end solutino of a given state. p.use matrix

#### How do you know what search you need to use ?
Most cases when it comes to what the program does, or what the problem is, if we have a graph from different notes, converting it into a matrix
and using A* algorithm would be more ideal, but in some sense you can conver that into a tree or some some other algorithm .

- What is the problem ?
- Why are we doing it ?
- What is the end goal for this?
- What bias are we working on ?

## Problem Types
### Types

#### Deterministic : Fully Observable => Single-State-problem
##### What is Single State problem ?

With Single State problems - You can do exact predictions on a given problem.

1.State: - the state is known exactly after any sequence of action

2.accessibility: - of the world all essential information can be obtained through sensors [ so it knows what path it has taken ?  ]

3.Consequences: - When the program / action does something, it knows what will happen - or the consequences of what may occour.

4.Goal: - For each known initial state, there needs to be some **goal** state that is reachible, and _guaranteed to be reachable_ Through Some set of Sequiences.

##### example :

**vaccum world**,

Refer to the notes within your notebook : look at the diagram.

- Limitations of the vaccum world :
- needs a certain area to scan, or some viable area.

- if the scanners are mislead or the information is not sound i.e not complete then it can change teh total
  consequences of the given action .

- indeterminism in the world, in action
Indeterminism is the idea that events are not caused, or not caused deterministically

##### Further information

> It is Deterministic, in a way that the AI program knows what state it will be in, and what options it would
> have.

- Chess Game, knowing all the information, like if a person moves a pawn, it knows it can only go take certain
  moves

- We know the next state would already be determined, and such that it is deterministic - Very clear Such that
  you know that each action has a determined state that it would go to .

A─────────────────►D

B─────────────────►C

You know that A leads to D no matter what and B leads to C no matter what, you dont have the option to switch .

#### Non-Observable : Conformant Problem  : Very similar to a baby trying to know the consequences for each action i.e learning from an expierence
##### What is a Conformat Problem ?

> Is  problem of finding a sequence of actions of achieving a goal in teh presence of uncertaintly within the initial state

1.State: - the _Initial_ State is unkown or there is a lack of certanity towards that given state

2.accessibility: -  There is no way of it to get the information from teh real world to the agent, so its facing the problem without further knoledge of what to do.

3.Consequences: - When the program / action does something, it has little knoledge to the sollution of the sequence it is supposed to get to.

4.Goal: - For each known initial state, there needs to be some **goal** state that is reachible, and _Unkown to be reachable_ Through Some set of Sequiences.

##### Example
- Meaning that the robot going into a new building : it has no idea about the layout of the building
- The robot would not know where to go, it would not know what exactly it has to do in that building .
  It mewans that the robot would have to navigate through the entire building first to map out and figure out where it needs to go.
    - This would imply that it owuld have to go through each room - room to room and need to navigate each process and create its own sequence to navigate a given problem.
- In this case it is learning from its own expierences Generate its own map

- Expierence Guided
- Once a expierence has been given - it should then compute and figure out how to deal with that.
  Working Cleaner Problem is a good example of this

#### NonDeterministic: Partial Observable => Contigency Problem >Very Complicated - Will not be explored too much on this module<
##### What is a contigency Problem ?

1.State: - **Unknown** In advance, may depend on teh outcome of the actions and changed in the enviorment _think of witcher3 when you have the option to go out with multiple females_.

2.accessibility: - Information about the world be be obtained through its execution, and its sensors - so it is a constant learning expierence from its own part.

3.Consequences: - What ever it does, it may not know what the issue or consequence may be, at the time of action.

4.Goal: - Tree set of goals, that it can go through, think of decision trees.

5. Contingency - Branching point in the tree of action, if x occours, what options do i have to avoid this given point

> The Exact State and prediction through its problem, is impossible to predict

> Some part of the current state may be unkown, i.e if you know a certain amount up to a point, consider the example :

A───────┬─►B ───────► ? ?  ? ? D
│          A and C both know that B Exist But B does not know where else to go - it would have to learn through its actions
│
C───────┘

It works depedent through its agent, Contigent plan policy to work towards : this is using a basis or some classifier for an algorithm to work upon.

1. Base Classifier
2. Basis Theorum to form the most likely possibility to form some given action.

#### Unkown State space Exploration problem
##### What is the Exploration problem ?
- No Information at all, you have no clue about the results of some given action, no clue about where you are
  going, it is based on what you have right now, and the learning epxierence. Again it comes down to ok, there is something here oo what can it do ... and learn from its own expierence, something similar to a self learning robot or something where it doesnt not know where to start.

## Vacume World
```comment
Look in book for examples - as it is better described there page 44
```

## Problems solved by classical Search Methods

- Knowing your enviorment -

1. Observable ?
    - Current state is known ?
      2. Discrete ?
    - From each state is there a finetly many states that you can jump to ? Executing states ? State wont change unless you make a move -> State would change .
      3. Deterministic ?
    - Each action has to have some action Classical Search has one action.
      4. Known?
    - Consequences of one state can lead to the next: and such that you know what is going on in classical  search
    - Possible actions of each action / state would lead to another Node - is this a vaired state ? does action A -> a known state or unknown state ?

## Single State Formulation

Single state formulation id described from the followings defined items .

### Set of states :
$$
{ At(a), At(b), At(c), ... At(z) }
$$

### Initial State
$$
  > At(a)
$$

### Set of actions ?
$$
{DriveTo(d)}
$$

### Transition Model - a successor function
$$
Result : {Set of States} States x Action -> State [Single State]
$$

### Goal test :
Test if something is within a list set, you can pop the values of a given list everytime you visited it
You can have a way to test a explict item : Refer to notes in the book.

### Path Cost
- Sum of each step is very important
- How much or what was the total cost to getting from point _a_ to point _b_

### Important Single state notes

**A solution is a path -> sequence of actions. from the initial state to a goal state**

**Optimal Solution is solutions with the lowest path cost**

## Real word state space ?
Real world is way to complex for our little brains, we not big brain man ...

So there has to be a way to fix this right ?

### Solution to the big scary world

- [x] State space needs to be _**abstracted**_ -> Problem Solving becomes easier
- [x] Abstracted State space is a set of real life states, but with a reduced complexity

Example of a real action that has been abstracted into prolog

```prolog
result(At(A), DriveTo(B), Final).
Final = B
```

In this example, we set a possible state, DriveTo, in which it will find all possible locations and actions from A to B and return B if it was true, such that it has reached its final destination.

- Something important to note _It must reach a real state_ otherwise this will fail .

## What does Abstracted State actually mean ?

Abstraction by defintion is breaking somethinh down to be more readible, same principle is applied here.

- when you abstract a given state: You have a set of real paths are are a solution in the real world - each
  abstracted action should be easier than the original problem .

## Sumary
- Real world problem in a search domain is the basis of how searches work

    - _Abstracting away real world details could be the following_

        - Set of states
        - Initial State
        - Set of actions that is being taken
        - Transition Model
        - Goal Test
        - Path Cost Function