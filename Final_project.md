Final Project: Movie Box Office Prediction
==========================================

Abstraction
-----------

This project intends to discuss two questions: 1) how to make movie
investment decision; 2) how much revenue is supposed to be generated if
invest. Therefore, two different dependent variables were used: binary
indicator of investment and continuous gross revenue of each movie. I
used both decision tree and multiple regression to construct models, and
then compare which method has stronger prediction power. In the result,
the best predictive results for both models was obtained through using
random forests method.

Introduction
------------

My favorite after-school activity is watching movies. However, by only
knowing the genres, actors, directors and budget of a movie, I am not
100% sure whether this will be a great movie, even though I’ve watched
thousands of movies. Sometimes, movies with famous actors may generate
low box office, sometimes low-budget movies could gain a huge amount of
profit. The film industry is always full of uncertainties, a small
amount of movies account for a huge amount of box office (see appendix
1). Thus, I am curious about how those investors make their decisions,
and if I were them how I should make decisions. Due to the uncertainty
of film industry, it is imperative to know which factors will influence
movie box office to minimize the risk associated with movie investment.

Data and Methodology
--------------------

The dataset I used in this report directly downloaded from Kaggel, and
the metadata is originally from IMDb dataset. This dataset included
around 5000 worldwide movies from 1963 to 2016. In this report, I
focused on movies after 1990 and US movie markets, which accounts for
72% observations. Secondly, because too many variables will make model
too complex to interpret, I used two methods to reduce dimensions (see
appendix 3): 1) I use principle component analysis to reduce dimension
of movie genres. I keep the first ten principle components, which
contains 70% variation. 2) I run first-order linear regression and drop
variables which are not statistically significant at 5% level in both
models. As a result, the post-prune dataset included two dependent
variables, and twelve independent variables (see table 1).

Table 1

    ## Skim summary statistics
    ##  n obs: 2745 
    ##  n variables: 14 
    ## 
    ## ── Variable type:factor ─────────────────────────────────────────────────────────────────
    ##  variable n_unique             top_counts ordered
    ##    invest        2 0: 1978, 1: 767, NA: 0   FALSE
    ## 
    ## ── Variable type:integer ────────────────────────────────────────────────────────────────
    ##                   variable      mean        sd
    ##     actor_1_facebook_likes   8624.81  17332.32
    ##     actor_2_facebook_likes   2311.59   4985.61
    ##     actor_3_facebook_likes    885.79   2095.6 
    ##  cast_total_facebook_likes  12948.29  21166.64
    ##    director_facebook_likes    858.33   3254.51
    ##     num_critic_for_reviews    171.29    126.89
    ##       num_user_for_reviews    344.04    418.95
    ##            num_voted_users 109906.79 157755.98
    ##                 title_year   2005         6.44
    ## 
    ## ── Variable type:numeric ────────────────────────────────────────────────────────────────
    ##      variable  mean    sd
    ##  aspect_ratio  2.11  0.37
    ##        budget 43.29 44.85
    ##         gross 58.52 73.54
    ##    imdb_score  6.34  1.04

### **Dependent Variables**

**Invest** This variable is an indicator, where it will take the value
“1” if its box office revenue is equal or higher than the double of the
budget or “0” otherwise. I will change the definition of “Invest” by
using different threshold later to check model robustness.

**Revenue** This variable is a continuous variable, represented in its
original form, which is called “gross” in the original dataset.

### **Independent Variables**

Independent variables are divided into three groups: movie features,
direct social media (IMDb) reaction features and indirect social media
(Facebook) reaction features.

Movie features

This group included four variables: year the movie released, genres of
the movie, aspect ratio of the movie and movie budget. The time trend
may affect the movie box office. For instance, movie released during the
depression periods may not generate high return and investors may also
be more conservative during that periods. Genres also play an important
role: comedy, drama and adventure movies usually generate more profit
than documentaries, and also those genres request for high budget due to
special effects (see appendix 2).

Direct social media(IMDb) reaction features

IMDb is an online database for films. People in the world could access
this website, review and rate any movies they want. It contains lots of
audiences’ direct reaction to a movie. This group of variables included
number of voted users, number of reviewed users on IMDb, IMDb score and
number of critical reviews for each movie.

Indirect social media(Facebook) reaction features

Facebook is an online social media, people could post, review and like
whatever they want, besides things directly related to films. This group
of variables included facebook likes of the director, facebook likes of
the first/second/third leading actor and total facebook likes of cast.
Instead of direct audience reaction, these features provided additional
information related to director, actors and cast for a specific movie.

Methods
-------

I used two methodologies in this project: random forests and forward
selection regression (logit regression for dummy dependent variable and
linear regression for continuous dependent variable), and then compare
RMSE and confusion table to identify which method has stronger
prediction power. In terms of forward selection, I set the scope
allowing interactions within each group of variables, since variables in
each group has stronger correlation than variables across groups. In
terms of randomness from train-test split, I run 100 times and average
the results.

Results
-------

### **Main Results**

**Binary Invest**

Table 2.1 and Table 2.2 represents average confusion table of random
forests and multiple regression. In multiple regression, if the
prediction value is larger than 0.7, which is the probability of
observing 0 value in “Invest” variable, it will be predicted as 1; if
not, it will be predicted as 0. Table 2 shows that random forest method
is much better than logit multiple regression, with around 20% error
rate compared to around 70% error rate from logit multiple regression.

Table 2.1 Confusion tree and error rate for random forest method

    confusion_tree

    ##       investhat
    ## invest   0   1
    ##      0 352  36
    ##      1  82  79

    error_rate_tree

    ## [1] 0.2149362

Table 2.2 Confusion tree and error rate for multiple regression method

    confusion_glm

    ##       investhat
    ## invest   0   1
    ##      0   4 384
    ##      1   0 161

    error_rate_glm

    ## [1] 0.6994536

**Continuous Revenue** Table 3 represents the average out-of-sample root
mean square error of different methods. It shows that random forest is
around 2 million dollars more accurate than linear multiple regression
model.

Table 3 RMSE for random forest and multiple regression (in million)

    colMeans(rmse_revenue_tree)

    ##   result 
    ## 39.97188

    colMeans(rmse_revenue_lm)

    ## result 
    ## 41.738

In general, random forest provide more accurate prediction. Figure 1
show the partial dependence of each variable on Revenue. For variable
“title year”, we find that it looks like U curve, and reach the lowest
point during 2008, when the great depression happened. For other
variables, the partial effect increase dramatically at the beginning and
then became stable in general, which means those variables have positive
effect with diminishing marginal effect.

![](Final_project_files/figure-markdown_strict/unnamed-chunk-8-1.png)

### Robustness

I change the definition of “Invest” by using different threshold to
check model robustness. Instead of using “revenue equal or higher than
the double of the budget” as a standard. I use the ratio of revenue to
budget equals to 1.8, 1.6, 1.4, 1.2 as different thresholds. Table 4
represents the average confusion table of different thresholds. The
result did not change a lot with error rate consistently around 20%-30%.

Table 4 Confusion table and error rate for different revenue to budget
ratio

    confusion_tree_1.8

    ##       investhat
    ## invest   0   1
    ##      0 340  27
    ##      1  94  88

    error_rate_tree_1.8

    ## [1] 0.2204007

    confusion_tree_1.6

    ##       investhat
    ## invest   0   1
    ##      0 297  39
    ##      1  98 115

    error_rate_tree_1.6

    ## [1] 0.2495446

    confusion_tree_1.4

    ##       investhat
    ## invest   0   1
    ##      0 261  53
    ##      1  99 136

    error_rate_tree_1.4

    ## [1] 0.276867

    confusion_tree_1.2

    ##       investhat
    ## invest   0   1
    ##      0 233  68
    ##      1  83 165

    error_rate_tree_1.2

    ## [1] 0.2750455

### Heteroskedasticity

High return usually accompanied with high risk, which, in statistics,
means that variance of predicted error increase with the increase of
revenue. From Figure 2, we can see that. the distribution of error terms
become more spread when the revenues increase.

![](Final_project_files/figure-markdown_strict/unnamed-chunk-11-1.png)

Conclusion
----------

In conclusion, random forests provides more accurate prediction for both
models, which might be a good choice if I want to predict future return.
All independent variables show positive correlation with diminishing
marginal effect. I also found: 1) the model is very robust when I change
the way the binary dependent variable is defined; 2) higher return is
accompanied with higher risk.

Appendix
--------

![](Final_project_files/figure-markdown_strict/unnamed-chunk-13-1.png)

![](Final_project_files/figure-markdown_strict/unnamed-chunk-15-1.png)

**Appendix 3.1: reduce dimension by PCA**

    ## Importance of first k=10 (out of 21) components:
    ##                           PC1    PC2     PC3     PC4     PC5     PC6
    ## Standard deviation     1.6463 1.5376 1.29144 1.16587 1.12376 1.06909
    ## Proportion of Variance 0.1291 0.1126 0.07942 0.06473 0.06014 0.05443
    ## Cumulative Proportion  0.1291 0.2417 0.32107 0.38580 0.44593 0.50036
    ##                            PC7     PC8     PC9    PC10
    ## Standard deviation     1.05604 1.03195 0.98561 0.93725
    ## Proportion of Variance 0.05311 0.05071 0.04626 0.04183
    ## Cumulative Proportion  0.55346 0.60417 0.65043 0.69226

**Appendix 3.2: reduce dimension by first-order linear regression**

    ## 
    ## Call:
    ## lm(formula = gross ~ (. - invest), data = movie)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -338.51  -19.42   -2.60   15.30  443.23 
    ## 
    ## Coefficients:
    ##                             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                1.602e+03  3.754e+02   4.269 2.04e-05 ***
    ## colorColor                 1.016e+01  5.396e+00   1.882 0.059926 .  
    ## num_critic_for_reviews     6.046e-02  1.417e-02   4.266 2.06e-05 ***
    ## duration                   9.764e-02  5.466e-02   1.786 0.074136 .  
    ## director_facebook_likes   -1.843e-03  2.751e-04  -6.698 2.56e-11 ***
    ## actor_3_facebook_likes    -8.224e-03  1.138e-03  -7.227 6.38e-13 ***
    ## actor_1_facebook_likes    -7.103e-03  6.951e-04 -10.220  < 2e-16 ***
    ## num_voted_users            1.694e-04  1.060e-05  15.983  < 2e-16 ***
    ## cast_total_facebook_likes  7.016e-03  6.940e-04  10.110  < 2e-16 ***
    ## facenumber_in_poster      -4.317e-01  3.992e-01  -1.081 0.279590    
    ## num_user_for_reviews       1.288e-02  3.579e-03   3.598 0.000326 ***
    ## content_ratingG            1.671e+01  1.679e+01   0.995 0.319859    
    ## content_ratingNC-17        3.808e-01  2.917e+01   0.013 0.989587    
    ## content_ratingNot Rated    6.245e+00  2.093e+01   0.298 0.765427    
    ## content_ratingPG           1.451e+01  1.558e+01   0.931 0.351686    
    ## content_ratingPG-13        1.286e+01  1.538e+01   0.836 0.403025    
    ## content_ratingR           -2.256e+00  1.535e+01  -0.147 0.883161    
    ## content_ratingUnrated      4.007e+00  2.128e+01   0.188 0.850639    
    ## budget                     6.212e-01  3.027e-02  20.525  < 2e-16 ***
    ## title_year                -8.171e-01  1.869e-01  -4.371 1.28e-05 ***
    ## actor_2_facebook_likes    -6.759e-03  7.355e-04  -9.189  < 2e-16 ***
    ## imdb_score                 1.444e+00  1.119e+00   1.290 0.197009    
    ## aspect_ratio              -2.750e+00  2.379e+00  -1.156 0.247830    
    ## movie_facebook_likes      -6.576e-05  5.524e-05  -1.190 0.234013    
    ## PC1                        5.175e+00  8.232e-01   6.286 3.78e-10 ***
    ## PC2                       -1.545e+00  6.483e-01  -2.384 0.017200 *  
    ## PC3                        2.029e+00  7.451e-01   2.723 0.006519 ** 
    ## PC4                       -1.498e+00  7.803e-01  -1.920 0.054921 .  
    ## PC5                       -4.205e-01  8.029e-01  -0.524 0.600484    
    ## PC6                        2.370e+00  8.037e-01   2.948 0.003221 ** 
    ## PC7                       -7.152e-01  7.938e-01  -0.901 0.367688    
    ## PC8                       -2.789e+00  8.369e-01  -3.332 0.000872 ***
    ## PC9                       -7.775e-01  8.383e-01  -0.927 0.353779    
    ## PC10                       1.089e+00  9.252e-01   1.178 0.239077    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 42.93 on 2711 degrees of freedom
    ## Multiple R-squared:  0.6633, Adjusted R-squared:  0.6592 
    ## F-statistic: 161.8 on 33 and 2711 DF,  p-value: < 2.2e-16

    ## 
    ## Call:
    ## glm(formula = as.numeric(invest) ~ (. - gross), data = movie)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.7703  -0.2897  -0.1421   0.3488   1.1233  
    ## 
    ## Coefficients:
    ##                             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                1.560e+01  3.488e+00   4.471 8.10e-06 ***
    ## colorColor                 3.845e-02  5.014e-02   0.767 0.443167    
    ## num_critic_for_reviews     7.092e-04  1.317e-04   5.385 7.87e-08 ***
    ## duration                  -4.589e-06  5.078e-04  -0.009 0.992792    
    ## director_facebook_likes   -1.218e-05  2.556e-06  -4.764 2.00e-06 ***
    ## actor_3_facebook_likes    -3.846e-05  1.057e-05  -3.637 0.000281 ***
    ## actor_1_facebook_likes    -2.733e-05  6.458e-06  -4.232 2.39e-05 ***
    ## num_voted_users            6.879e-07  9.847e-08   6.986 3.55e-12 ***
    ## cast_total_facebook_likes  2.726e-05  6.448e-06   4.227 2.45e-05 ***
    ## facenumber_in_poster       3.417e-03  3.709e-03   0.921 0.356969    
    ## num_user_for_reviews       6.143e-05  3.325e-05   1.847 0.064795 .  
    ## content_ratingG            2.412e-01  1.560e-01   1.546 0.122243    
    ## content_ratingNC-17       -2.887e-01  2.711e-01  -1.065 0.286968    
    ## content_ratingNot Rated   -7.660e-02  1.945e-01  -0.394 0.693720    
    ## content_ratingPG           2.402e-01  1.447e-01   1.660 0.097044 .  
    ## content_ratingPG-13        1.914e-01  1.429e-01   1.339 0.180549    
    ## content_ratingR            7.656e-02  1.426e-01   0.537 0.591444    
    ## content_ratingUnrated      1.359e-01  1.977e-01   0.687 0.492001    
    ## budget                    -4.549e-03  2.812e-04 -16.175  < 2e-16 ***
    ## title_year                -7.262e-03  1.737e-03  -4.181 3.00e-05 ***
    ## actor_2_facebook_likes    -2.816e-05  6.834e-06  -4.120 3.90e-05 ***
    ## imdb_score                 2.808e-02  1.040e-02   2.701 0.006965 ** 
    ## aspect_ratio              -7.160e-02  2.211e-02  -3.238 0.001217 ** 
    ## movie_facebook_likes      -8.844e-08  5.133e-07  -0.172 0.863220    
    ## PC1                        2.293e-02  7.649e-03   2.999 0.002738 ** 
    ## PC2                       -1.200e-02  6.024e-03  -1.991 0.046537 *  
    ## PC3                        1.431e-02  6.924e-03   2.067 0.038789 *  
    ## PC4                       -1.096e-02  7.250e-03  -1.512 0.130613    
    ## PC5                        2.937e-02  7.461e-03   3.936 8.49e-05 ***
    ## PC6                        1.459e-02  7.468e-03   1.954 0.050862 .  
    ## PC7                       -1.244e-02  7.376e-03  -1.687 0.091793 .  
    ## PC8                       -2.922e-02  7.777e-03  -3.758 0.000175 ***
    ## PC9                        1.059e-02  7.790e-03   1.359 0.174256    
    ## PC10                       7.980e-03  8.597e-03   0.928 0.353343    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for gaussian family taken to be 0.1591216)
    ## 
    ##     Null deviance: 552.69  on 2744  degrees of freedom
    ## Residual deviance: 431.38  on 2711  degrees of freedom
    ## AIC: 2780.2
    ## 
    ## Number of Fisher Scoring iterations: 2
