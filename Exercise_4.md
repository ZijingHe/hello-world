Question 1 Clustering and PCA
-----------------------------

![](Exercise%204/unnamed-chunk-2-1.png)![](Exercise%204/unnamed-chunk-2-2.png) 

Figure 1 and Figure 2 are not very different; however, Figure 2
(clustering) method is more capable of distinguishing the red wine from
the white wine, since there is some overlap in Figure 1.

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   3.000   5.000   6.000   5.818   6.000   9.000

Although, there are 10 scales in wine quality, only 3-9 appeared in this
dataset. Then, I use k-means++ to divide these observations into 7
clusters.

![](Exercise%204/unnamed-chunk-4-1.png)

Figure 3 is very noisy, clustering method does not work to distinguish
wine quality.

Question 2 Market Segementation
-------------------------------

First, I delete the random user identity, chatter, uncategorized, spam
and adult colunms, to reduce the noise as much as possible.

![](Exercise%204/unnamed-chunk-5-1.png) 

The audiences of NutrientH20 are roughly clustered to two parts. The
first part is audiences who are interested in sports, religion, food,
family, parenting and school. Another part is the rest interests. The
best strategy is focusing the first cluster, because the first cluster
account for heavier weights, and with less interests, which means easier
to target these customers.

Question 3 Association Rules for Grocery Purchases
--------------------------------------------------

First, I plot a barplot of top 20 most frequently purchased items. This
graph gives me a general picture of transactions.

![](Exercise%204/unnamed-chunk-7-1.png)

I choose support rate no less than 0.1, which means the probability of
transactions that contain all these items should not be lower than 10
percent. In total, there are around 15000 transactions, which means I
focus the combination which happened more than 1500 times. This should
be appropriate because transcations which happened frequently are more
meaningful to research. In terms of the confidence rate, it should be
larger than support rate. The lower the confidence rate, the more
association could get. When confidence rate is lower than 0.6, the
number of association does not go up. Thus, 0.6 confidence is a good
choice.

![](Exercise%204/unnamed-chunk-9-1.png) 

There are six associations more likely to happened: pip fruit and tropical
fruit, citrus fruit and tropical fruit, root vegetables and other
vegetables, butter and whole milk, tropical fruit and root vegetables,
curd and whole milk. Compare to randomly choose a buyer who buy any
association, buyers buy one item out of any association are at least
twice more likely to buy another item in corresponded association.

    ##      lhs                   rhs                support    confidence
    ## [1]  {pip fruit}        => {tropical fruit}   0.01268305 0.26075269
    ## [2]  {tropical fruit}   => {pip fruit}        0.01268305 0.18798450
    ## [3]  {citrus fruit}     => {tropical fruit}   0.01248692 0.23464373
    ## [4]  {tropical fruit}   => {citrus fruit}     0.01248692 0.18507752
    ## [5]  {root vegetables}  => {other vegetables} 0.02536611 0.36194030
    ## [6]  {other vegetables} => {root vegetables}  0.02536611 0.20388860
    ## [7]  {butter}           => {whole milk}       0.01438285 0.40366972
    ## [8]  {whole milk}       => {butter}           0.01438285 0.08754477
    ## [9]  {tropical fruit}   => {root vegetables}  0.01098326 0.16279070
    ## [10] {root vegetables}  => {tropical fruit}   0.01098326 0.15671642
    ## [11] {curd}             => {whole milk}       0.01261768 0.36832061
    ## [12] {whole milk}       => {curd}             0.01261768 0.07680064
    ##      lift     count
    ## [1]  3.864800 194  
    ## [2]  3.864800 194  
    ## [3]  3.477820 191  
    ## [4]  3.477820 191  
    ## [5]  2.909216 388  
    ## [6]  2.909216 388  
    ## [7]  2.457036 220  
    ## [8]  2.457036 220  
    ## [9]  2.322805 168  
    ## [10] 2.322805 168  
    ## [11] 2.241875 193  
    ## [12] 2.241875 193

We can visualize the association rules through network graph. The larger
the label size, the more frequent this item appeared in a transaction,
which is another representation of the barplot. The dark the color of
the edge, the higher the lift of the association, which corresponded to
what I found.
![](Exercise%204/network.png)
