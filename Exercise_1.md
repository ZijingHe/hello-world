Question 1 -- Green Buildings
=============================

In general, there are some confounding variables through which green
certification could affect rent indirectly. We could not simply divide
whole sample into two parts by whether the building is green certified
or not. I will first clean the dataset and then present some
visualization graphs to support my analysis.

In terms of cleaning the data, I partly agree with the recommendation in
the question. The distribution of leasing rate is kind of weird for
non-green buildings which make them incomparable with green buildings.

![](Exercise%201/unnamed-chunk-2-1.png)

Besides leasing rate, green buildings are younger than non-green
buildings on average. Also, we can see the trend for older buildings at
the very right part of the graph. Older buildings, in general, generate
lower rent and are usually non-green buildings, which might bring the
average/median rent of non-green buidings down if we count them.

![](Exercise%201/unnamed-chunk-3-1.png)

Meanwhile, older buildings are more likely be renovated, extra cost may
also affect the rent.

![](Exercise%201/unnamed-chunk-4-1.png)

Thus, we clean the dataset by delete rows which the leasing rate is
lower than 10 and the age of buildings is higher than 116. The threshold
116 set equals to the age of the oldest green buildings.

Graphs below show whether the rent difference between non-green
buildings and green buildings (revenue difference we care) is affected
by other confounding variables. For size, stories and the contract type,
the rent differences do not deviate much when the size/stories/contract
type changes.

![](Exercise%201/unnamed-chunk-6-1.png)![](Exercise%201/unnamed-chunk-6-2.png)![](Exercise%201/unnamed-chunk-6-3.png)
The differences of rent are larger for buildings which have undergone
substantial renovations during their lifetimes. However, the cost
generated from renovation might also be different, so the effect on rent
is ambiguous.
![](Exercise%201/unnamed-chunk-7-1.png)

The differences of rent are larger for buildings with low quality or
with amenities.

![](Exercise%201/unnamed-chunk-8-1.png)![](Exercise%201/unnamed-chunk-8-2.png)

For the demographical variables, in the same cluster, those building
have the same values. Thus, analysis one of them is representative. The
market rent is positively correlated with cluster rent. With the
increase of cluster rent, the variation of non green buildings become
larger, this may generate an indirect effect from green certification on
rent

![](Exercise%201/unnamed-chunk-9-1.png)

In conclude, if we want to compare apples-to-apples, it is important to
focus on the same region (it should be larger than a quarter mile to
include more comparison data). Also, some features of building like
renovation, quality and amenities are also highly correlated with green
certification. Thus, to do a better analysis, we need more information
about the building. Not only about the stories and locations from the
question, but also other feature information, such as the quality of the
building, whether there are amenities in the buildings.

Question 2 -- ABIA
==================

In this question, I will try to answer the question about the best time
to fly, both the best time of a day and the best time of a year. To
answer them, I will both illustrate the probability of delay in a time
period, and if delay, how long on average need to wait.

We cut the continuous scheduled departure time in to 24 categories by
hour of a day. Since there is no scheduled departure flights from 0 to 5
am, the comparison starts from 6am.

In figure 1 and figure 2, we can see the best time of a day to fly is
during 6am to 9 am with probability of delay lower than 30%, and if
delay, wait less than 30 minutes on average.

![](Exercise%201/unnamed-chunk-12-1.png)![](Exercise%201/unnamed-chunk-12-2.png)

In figure 3 and figure 4, the best time of a year to fly is from
September to November with probability of delay lower than 30%, and if
delay, wait less than approximately 20 minutes on average.

![](Exercise%201/unnamed-chunk-13-1.png)![](Exercise%201/unnamed-chunk-13-2.png)

Question 3 -- KNN
=================

Figure 1 and Figure 2 shows a plot of RMSE versus K for car trim level
550 and a plot of the fitted model at the optimal K value.

![](Exercise%201/unnamed-chunk-15-1.png)![](Exercise%201/unnamed-chunk-15-2.png)

Figure 3 and Figure 4 shows a plot of RMSE versus K for car trim level
65AMG and a plot of the fitted model at the optimal K value.

![](Exercise%201/unnamed-chunk-16-1.png)![](Exercise%201/unnamed-chunk-16-2.png)

Since the optimal K will be affected by different random subsmaple we
choose. On average, optimal K of the second subsample is relatively
smaller than that of the first subsample. The difference of the optimal
K values is resulted from sample size difference. The second sample
contains less sample size. Thus, smallest out-of-sample MSE corresponded
to smaller K value.
