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
```comment@@a
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
