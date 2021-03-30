# Interview Questions: Statistics

## Probability of winning dice game

Game: Two players take turns rolling a die. The first one rolling a 6 wins.
Question: What is the probability that A wins if A begins rolling the dice.
## Solution

Probability that A wins:
$$ P(A) = \frac{1}{6} + \frac{1}{6} (\frac{5}{6})^2 + \frac{1}{6} (\frac{5}{6})^4 + ... + \frac{1}{6} (\frac{5}{6})^{2n} $$

$$ \begin{aligned}
    P(A) &= \frac{1}{6} (1 + \sum_{i=1}^{\infty}(\frac{5}{6})^{2i}) \\
         &= \frac{1}{6} (\sum_{i=0}^{\infty} (\frac{25}{36})^{i}) \\ 
         &= \frac{1}{6} (\frac{1}{1-\frac{25}{36}}) \\
         &= \frac{6}{11}
   \end{aligned}
$$