  title: prolog_notes_QuestionSheets
  description:
  authors: viv
  categories:
  created: 2022-02-17
  version: 0.0.11

# Week 4 and 5 Exercise 3 :

## Question 1
> Write a program all members( +X, +Y ) which checks whether all members of a given list
> X are members of another given list Y
### ALl Members
```prolog
all_members([],_). % if list is empty, then all members are in list
all_members([H|T],L):-
  member(H,L), all_members(T,L). % if head is in list, then check the rest of the list
```
### What does it do
We split the Head and tail, and have another List L, that is out Unifier
We check if the Head of the List is in L, and then we recurse over all_members
## Question 2
> 2. Write a program pairs( +X, ?Y ) which, given a list X of numbers, constructs a list Y of
> the same length such that
> each member of Y is (U, V) when the corresponding member of X is N
> and U is N-1 and V is N+1.
### Get Pairs of Values with a List and a unifier : pairs(+X, ?Y)
```prolog
pairs([], []).
pairs([H|T], Y) :-
  pairs(T, Y1),
  H1 is H - 1,
  H2 is H + 1,
  Y = [(H1, H2)|Y1].
```
### What does it do ?
_This was annoyling confusing_
From a recursive standpoint it does the following procedure

```prolog
initial_call -> pairs([1,2,3,4,5], Y)
Rec_1 -> pairs([2,3,4,5], Y1)
Rec_2 -> pairs([3,4,5], Y2)
Rec_3 -> pairs([4,5], Y3)
Rec_4 -> pairs([5], Y4)
Rec_5 -> pairs([], Y5)

▲ Y = [(0,1),(1,2),(2,3),(3,4),(4,5)]
│ Y1 = [(1,3),(2,4),(3,5)]
│ Y2 = [(2,4),(3,5)]
│ Y3 = [(3,5)]
│ Y4 = [(4,5)]
│ Y5 = []
│ Y = [(0,1),(1,2),(2,3),(3,4),(4,5)]
```

From Initial call, it will first cut down the list due to its initial recurisive call .
within each recursion like Rec_1 or Rec_2 , you we define a New Y in theory, think of y1 y2 ... as a new Y such that in this case we have _**5 instances**_ of Y

Here are the following values that are returned
```prolog
▲ REC 1 = (1,3)
│ REC 2 = (2,4)
│ REC 3 = (3,5)
│ REC 4 = (4,5)
│ REC 5 = []
│ Y1 = [(1,3),(2,4),(3,5)]
```

Rec_5 will return a empty list - Base case has been met
Rec_4 will then create H1 and H2
- H1 = 4
- H2 = 5
  we then call that on Y1 defined within the pairs so our Y5 pretty much that was called, in this case it is an empty List so no we dont combine we just combine "[(4,5),]" atm

Rec_3 Will Create
- H1 = 3
- H2 = 5
  _Why is H2 5?_
  Well H2 is part of the head right ? our returned value is actualy 4, from the previous recursive call . Due to Y3 being returned.

... Repeat
Final Step where it all gets added up
Each pair will then be pushed correctly, we negate the empty list and we return our values that was computed

Y = [(0,1)(1,2)(2,3)(3,4)(4,5)]

### how do you get (0,1) and (1,2) and (2,3) and (3,4) and (4,5) ?
- Y4 adds (4,5) to the list
- Y3  takes 3 from Y4 and adds it to the list becoming 3,4
- Y2 takes 2 from Y3 and adds it to the list becoming 2,3
- Y1 takes 1 from Y2 and adds it to the list becoming 1,2
- Initial Y takes 0 from Y1 and adds it to the list becoming 0,1
```
Y5 = [] -> Y4 = [(4,5)] -> Y3 = [(3,5)] -> Y2 = [(2,4),(3,5)] -> Y1 = [(1,3),(2,4),(3,5)] -> Y = [(0,1),(1,2),(2,3),(3,4),(4,5)]
```
  Which Gives us Y once it is added to the end

## Question 3
> 3. Write a program arbpairs( +X, ?Y ) which, given a list X of numbers, constructs a list Y
> of the same length such that
> each member of Y is (N, L) when the corresponding member of X is N
> and L is either N or 2N.
> Y = [(2,2),(4,4)]
> Y = [(2,4),(4,4)]
### ArbPairs
```prolog
arbpairs([], []).
arbpairs([H|T], Y):-
  arbpairs(T,Y1),
  N is H,
  (N mod 2 =:= 0 -> L is N; L is 2*N),
  Y = [(N,L)|Y1].
```

### New Tools learnt
#### Comparison operator
```prolog
N mod 2 =:= 0
```
this is a comparision operator, that would check if two values are equal
in this case we are checking the command N Mod 2 == 0

Pythonicly It would be like
```python
N = 10
return N % 2 == 0
```
Returning True similar principle above

#### if else statement (sorta)
```prolog
(N mod 2 =:= 0 -> L is N; L is 2*N),
```
Using the Comparision Operator - you then can say the following
if N mod 2 is true then L is N OR L is 2 * N

Pythonicly we can say
```python
if __name__ == "__main__":
  import random

  N = 10
  L = 0
  options = [N, 2 * N]
  if N % 2 == 0:
      L = sorted(options, key=lambda x: random.random())
  print(L[0])
```
The "->" acts more of an if else, without the if statement
### Note
_Above Code does not do what it supposed to do, but is a nice touch to what you can do_
### Answer for question 3
#### Code
```prolog
arbpairs( [], [] ).
arbpairs( [h|t], [ (h,h) | y] ) :- arbpairs( t, y ).
arbpairs( [h|t], y ) :-
  h1 is h * 2,
  arbpairs( t, y1 ),
  y = [(h,h1)|y1].
```
#### What does it do ? _This was really annoying o_o_
```prolog
arbpairs( [h|t], [ (h,h) | y] ) :- arbpairs( t, y ).
```

```comment
what does the (h,h) part do in arbpairs( [h|t], [ (h,h) | y] ) :- arbpairs( t, y ).
(h,h) is a member of the list [(h,h)|y] which is the result of arbpairs(t,y) -> arbpairs( [], [] ). -> [] is the result of arbpairs( [], [] ).
this gets all the pairs, or valid pairs for one tuple -> (2,2) or (4,4) for lhs and rhs
```

```prolog
arbpairs( [2,4], Y ) -> arbpairs( [4], Y1 ) -> arbpairs( [], Y2 ) -> Y = [(2,2),(4,4)]
Y1 = [(4,4)]
Y2 = []
Y = [(2,2),(4,4)]
```

then we have our second statement
```prolog
arbpairs( [h|t], y ) :-
  h1 is h * 2,
  arbpairs( t, y1 ),
  y = [(h,h1)|y1].
```
if we have arbpairs( [2,4,6], Y ) this statement will do ?
this gets all the pairs, or valid pairs for one tuple ~~> (2,2) or (4,4) for lhs and rhs
arbpairs( [2,4,6], Y ) -> arbpairs( [4,6], Y1 ) -> arbpairs( [], Y2 ) -> Y = [(2,2),(4,4)]
Y1 = [(4,4),(6,6)]

Due to how prolog works, we would end up getting all pairs, within a given call shown below
```prolog
?- arbpairs([2,4],Y).
Y = [(2, 2),  (4, 4)] ;
Y = [(2, 2),  (4, 8)] ;
Y = [(2, 4),  (4, 4)] ;
Y = [(2, 4),  (4, 8)].
```

## Question 4
> 4. Write a program replace wrap/2, which replaces every member X of a list with wrap(X):
> ?- replace_wrap([a,b,b,c], Res).
> Res = [wrap(a),wrap(b),wrap(b),wrap(c)]
### Code
```prolog
replace_wrap([],[]).
replace_wrap([H|T], [wrap(H)|T1]):- replace_wrap(T,T1).
```
### What does it do ?
So once again we are reducing down our list, with the base case being [ ]
```prolog
│ replace_wrap([a,b,c], Y)
│ replace_wrap([b,c], Y1)
│ replace_wrap([c], Y2)
▼ replace_wrap([], Y3)
```
From a top down once again, recall what our function is taking ?
[wrap(H)| T1]
```prolog                   ▲
│ Y = [wrap(a),wrap(b),wrap(c)]│
│ Y1 = [wrap(b),wrap(c)]       │
│ Y2 = [wrap(c)]               │
▼ Y3 = []                      │
```

We return up  Such that, for each Y we will have a T1, being wrap(c) on T
**call replace_wrap([a,b,c], Res)**
```comment
│  Stage_1 -> replace_wrap([a,b,c], []).
│  Stage_2 -> replace_wrap([a,b,c], [wrap(a)|[]].
│  Stage_3 -> replace_wrap([b,c], [wrap(a),wrap(b)|[]].
│  Stage_4 -> replace_wrap([c], [wrap(a),wrap(b),wrap(c)|[]].
│  Stage_5 -> replace_wrap([], [wrap(a),wrap(b),wrap(c)|[]].
▼  Stage_6 -> replace_wrap([], [wrap(a),wrap(b),wrap(c)|[]].
```

## Question 5
### Code
_At this point i dont even know what im doing that makes this work 0_0_
```prolog
even_members([],[]).
even_members([H|T], [H|T1]):-
  length([H|T], Len),
  Len mod 2 =:= 0,
  even_members(T, T1),
  T1 = T1, !.
even_members([H|T], T1):-
  length([H|T], Len),
  Len mod 2 =:= 1,
  even_members(T, T1),
  T1 = T1, !.
```
### What does it do ?

## Question 6
### Code
```prolog
```
### What does it do ?