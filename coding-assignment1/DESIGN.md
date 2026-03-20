# Lab Assignment 1 25/1
 
## Algorithm
 
I looked at all the training data and it made sense to use the columns to figure out a pattern. The idea was that if the CPU just played something, it probably has a tendency to follow it up with a specific move, so I tracked how often each move followed each other move across the whole history. Then for each round, I just looked at what the CPU last played, found what it most commonly plays after that, and played whatever beats it.
 
## Design 
 
The core of the algorithm is a 3x3 transition matrix. Each row is what the CPU just played, each column is what it plays next, and the numbers are how many times that transition happened in the training data:
 
|  | → Rock | → Paper | → Scissors |
|---|---|---|---|
| **Rock** | 0 | 15 | 17 |
| **Paper** | 15 | 0 | 18 |
| **Scissors** | 17 | 18 | 0 |
 
One thing I noticed right away is the CPU never really repeats the same move twice, majority of diagonal entries are 0. Based on the counts, the algorithm predicts:
 
- After CPU plays Rock → expect Scissors → play **Rock**
- After CPU plays Paper → expect Scissors → play **Rock**  
- After CPU plays Scissors → expect Paper → play **Scissors**
 
If there isn't enough history yet, it just plays randomly as a fallback.
 
## Results
 
| | Count | % |
|---|---|---|
| Wins | 35 | 35.0% |
| Losses | 23 | 23.0% |
| Draws | 42 | 42.0% |
 
Win rate came out to 35% against a random baseline of 33.3%, with a net score of +12. The loss rate dropped to 23% which is pretty good compared to the 33% mark you'd expect from random play.
 
## Reflection
 
Looking back at it, the training data made it pretty clear what was going on once I laid it out. I'm not totally sure what else could've been done differently, except maybe looking at the last two moves instead of just one would've helped the algorithm pick up on longer patterns, but what I had was enough to get above the baseline. The main thing I'm taking away is that even a simple pattern-tracking approach can work if the data actually has a pattern in it, which this one did.