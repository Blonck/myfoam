# Metrics

## Lift Score

The lift score of a certain subset of all samples is the response rate in this subset normalized by the average response rate.

The response rate is the positive reaction rate of the model.

$$ \frac{P}{P + N} $$
where:

$$
P: \textrm{positives} \\
N: \textrm{negatives}
$$

For the lift score, one sort the results of the model according to the prediction probability and split them up in quantiles (usually 10: decile).
Than each quantiles lift score is evaluated. The lift score of each quantile gives now how much better than random one would be when selecting only
samples of that quantile.

[https://towardsdatascience.com/model-lift-the-missing-link-70eb37460e67]
