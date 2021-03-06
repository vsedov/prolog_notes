  title: index
  description:
  authors: viv
  categories:
  created: 2022-03-15
  version: 0.0.11

# Adverarial Search
This is a different type of search program where you can use this to search a game or have some problem solving factor
It focuses on where teh goals of the programs, where you have a conflict in some sense

- Search algo where the goals in teh game have a conflict, like a 2 player game, think of tenken ? Which programming can win the fight ?

- Fun Fact this uses heaps, because heaps goes brrrr: That said it uses a min heap . Where you store the chances or have a identifier to define which factor is more optimal.

- There are certain search stratergies, for which activity and what search ti would have to go through .

- It uses Alpha beta prunning [](%20Will%20describe%20later%20down%20the%20line%20)

## Games
How do you deal with games and search problems together ?

Games can be very unpredictable, so how do you know what option to go in :think:
There are so many factors :

- Time limit => unlikely to find goal, so it must approximate based on the current data
- Unpredictable factor  => Solution is based on a stratergy between each other
- Glitches ?

There are different type of games
```comment
                              Deterministic                             Chance
 ───────────────────────┬────────────────────────────────┬───────────────────────────────────────────
  Perfect information   │    Chess , checkers , go       │    backgammon  monopoly beyblade
                        │    othello                     │
────────────────────────┼────────────────────────────────┼───────────────────────────────────────────
                        │                                │
 imperfect information  │    Battleships blindtictacto   │  bridge, procker, scrabble nuclear war
                        │                                │
```

1. Options
- [x] Focus Games : they are games where you knoe everything, they are deterministic without random chance, there
      is somethign where you know something will ocour Main Focus

- [x] Imperfect games, are somethign with a large ammount of randomness, but some times you have a point or you
      know what might win or not, even though there is large ammount of chance to it

## How is Game Search defined ?
Game Search is very similar to tree search

Game search is formally defined as below
$$
S_0 is initial state

Player(s): defines whcih player has the move in the state so like a boolean tick in some sense

Actions(s): returns the set of legal moves in a state

Result(s,a): transition model that returns the result of a move

Terminal - Test(s): is true if the game has terminated and false otherwise

Utility(s,p): Function returning 1 or 0 or 1/2 if it is a draw
$$

We say a _Zero Sum_ Game is a game where the total payoff to all player is teh same for every instance of a game .
A really good example of this would be **Chess**, in the instance that chess is a zero sum game - where each move would determine which basis you would work in

## Min Max
- Perfect play for determinsitic games, are known as Pefect information games

- We can say we can use a min max heap to define the highest and minmax value - so the principle of achieving teh
  most achievable and most ideal placement of your given value
Which value is teh lowest time / kind

["Example Scinario"](img/2022-03-15-20-31-09.png)

Example here you have 2 player game, with A,B, C ,D are states and a_i b_i ... are possible movies they can make
Each move would change another state , that we have a max and min heap

_Look at notes in book for minmax_ Hard to define minmax and game theory in norg format.

#### Complexity and time
##### Space
O(BM)
##### Time
O(B^M)
From Single point of view this is going through the max depth of your value

##### Optimal
Yes
#### Example Code
```lua
-- Not lua code but nice syntax so why not
function minmax(position, depth, maximizingPlayer)
   if depth == 0 or game_over in possition then
      return static evaluation of position
   end

   if maximizingPlayer then
      maxEval = -Inf
      for each child of position
          eval = minmax(child,depth-1, false)
          maxEval = max(maxEval, eval)
       return maxEval
    else
       minEval = +infinity
       for each child of position
          eval = minmax(child, depth - 1, true)
          minEval = min(minEval , eval)
       return minEval
   end
end
```

## Alpha beta pruning
From a single stand point alpha beta pruning evaluates your max and min values
You cut out a whole branch if you know something might not get even evaluated in teh first place

You have this min and max and you have this alpha and beta value

What you do is the following code
```lua
    -- Not lua code but nice syntax so why not
    function minmax(position, depth,alpha, beta, maximizingPlayer)
       if depth == 0 or game_over in possition then
          return static evaluation of position
       end

       if maximizingPlayer then
          maxEval = -Inf
          for each child of position
              eval = minmax(child,depth-1,alpha, beta false)
              maxEval = max(maxEval, eval)
              alpha = max(alpha, eval)
              --- New Code
              if (beta <= alpha) then
                 break
              end
           return maxEval
        else
           minEval = +infinity
           for each child of position
              eval = minmax(child, depth - 1, true)
              minEval = min(minEval , eval)
              --- New code
              beta = min(beta, eval)
              if beta <= alpha then
                 break
              end
           return minEval
       end
    end
```

What this does is some what like dynamic programming in a sense, what you have is this list, or some values alpha and beta, you go over each of your loops and avlues, and you check if beta is less than alpha, because you know that white, whish is max will only take the max between the two values, if you know that you can stop teh whole iteration at that point.

What you should think of is that you make some pointer or some hold of a value, in that case what would happen is that, your first depth search , or your lowest depth will return the max value of that depth or LHS in this instance if you have a branch that is split between multiple values
Once you do that, all you have to do is check if the next branch, will be greater, or less than,  say you have the following tree
```comment

                                         Max  Of below
                                         │
                      ┌──────────────────┼───────────────┐
                      │                  │               │
                      │                  │               │
                      ▼               2 <= 3            [2,2]  Min
                     3, 3                │               │
                  ┌───┼────┐             │               │
                  │   │    │        ┌────┘               │
                  │   │    │        │   This does     ┌──┼─┐
                  │   │    │        │  Not evaluate   │  │ │
                  ▼   ▼    ▼        ▼                 ▼  ▼ ▼     Max
                  3   12    8       2                 14 5 2
                                                     ───────►
                                                     You go through each one till you reach 2
                                                     if you had [2 5 14 ]
                                                     you would then prune the rest ...
```

### Extra information about pruning

Pruning does not affect the final result, Why is that ?
Because im **BATMAN** well yes and no

you see, you have this set of evaluation right, max min max min their are certain rules black and white can follow through with

so like look at the example above the abstracted version would look like this :

```comment
   Max of below
      │
      │
      ▼
A set of Min values of below
      │
      │
      │
      ▼
A set of Max values of below
```
Using this logic, say we have oour LHS give us a min value of 3 our middle gives us our min of 2, by default we know that this function evaluates minimum values, if our value is 2 we cant do anything else so we have to skip it
in skipping it we take out the rest of the branchs, because say we evaluate 2, and the next val is -1 , tf is that going to do, our main function or top level function is taking hte max of our values not the min ... so in that scinario we know we just skip it, because it does not apply to what we are going to do .

Compared to the next principle or the RHS where our first min value was 14, omg we found a value greater than 3 ? well yes but we have to take the min of those values right, in that case the min is 2 and hence we ditch it

if 2 was in front then we could prune cause pruning is op

## Outline: phantom pruning episode 1
### Time:
Time is based on our ordering so we can in theory with pruning reduce everything with O(B^[](m/2)) which is nuts thats legit half of our problem solved
### Space
There is a limit though, one of them being space and resource limits, one of the main issues with this is that the limit behind  this is too much, or that if you have to explore each node, you would use more memroy, which is not ideal.
### Optimal
Yes it is optimal, we are legit halving our search time >.<

Overall i think this is good, but there are very important problems, and i think search and sorting algorothm would play a massive part into how this would work overall.

$Digression : exact values dont matter$
**Behaviour is always preserved**
_OMG_ How ? whoaaa nade kore ???? [](Shock%20FACE)
Well they are preserved under any monotonic evaluation ?

wtf does monotonic mean ?
> monotonic function is a function between ordered sets that preserves or reverses the given order. This concept first arose in calculus, and was later generalized to the more abstract setting of order theory
Welp their you go, so if its in order you are a o k
_

# Overall
1. Game theory is weird
2. Perfect game is impossible, but you have to be approximate with your values and estimation
3. Good idea to think about what to think about, and then what that is thinking about, and then what that is thinking about, dam this is confusing isnt it
4. Uncertaintiy contraints asigns each value to its state
5. Optimal decision depends on teh second dude

Games are to Ai as grand prix is to automobile design, but hey we are getting there