Question 1: Saratoga House Prices
=================================

To build a better model which could outperforms the medium model, I
think there may be three improvements I could make.

I will discuss the reasons for each improvement. Also, each improvement
includes a group of add-on variables (new variables or interaction
terms). I will add each group on the original medium model separately
and check whether it will outperform the medium model or not.

The first improvement is adding three new variables: landvalues,
waterfront and newconstruction. The house price is highly correlated to
where the house located. A good place usually corresponded to a higher
land values, and waterfront could be an indicator of a good location.
New construction, which means it's a brandnew house and nobody stays
before, indicates a good function of utilities. It's may a factor which
increases house price. The results (V1 for medium model, V2 for medium
model with improvement) turns out to be very good, the out-of-sample
RMSE is 7000 smaller than the medium model, which means it is around
7000 dollar more accurate than the medium model. These three omitted
variables may be a strong driver of house prices.

    ##       V1       V2 
    ## 65953.82 58713.54

The second improvement is adding on interaction between bedrooms and
bathrooms. I think a high value house should do well in balancing
resource, which means the ratio of bathrooms to bedrooms should not be
too small, for instance, a four-bedroom house usually have at least two
bathrooms. However, the result (V1 for medium model, V2 for medium model
with improvement) turns out that this interaction may not be a strong
driver of the house price.

    ##       V1       V2 
    ## 66220.73 66910.85

The last improvement is adding on interaction between living area and
fuel, interaction between living area and heating, and interaction
between living area and central air. Different heating system, different
fuel system type and whether it has central air conditioning, will
affect the correlation between living area and hour price. For example,
it may be the case the heating system A is more efficient for big house,
thus, the effect of living area on house price will be different between
big house and small house due to different cost generated from heating
system. This kind of typical case may also apply to different fuel
system, and whether air conditioning or not. These interactions (V1 for
medium model, V2 for medium model with improvement) turn out to have
some contributions to improvement of the model.

    ##       V1       V2 
    ## 65715.52 64980.04

The final model is built by adding the first improvement and the third
improvement to the original medium model. The out-of-sample RMSE (V1 for
medium model, V2 for medium model with improvements) is 8000 smaller
than the medium model, which means my hand-build model is around 8000
dollars more accurate than the mdium model.

In conclusion, when the local tax authority predicted market values for
properties, they should consider the area of the house (lot size, living
area), also the location of the house (land values, waterfront) , the
inside construction features ( bedrooms, bathrooms, rooms, new
construction) and the type of heating and fuel system (heating, fuel,
air conditioning, fireplaces). The more detail correlation, specific to
a certain value, is presented below.

I then turn this hand-built linear model into a KNN model, the plot
shows that the minimum out-of-sample RMSE is bigger than
60000, which is not better than my hand-build linear regression model.

![](Exercise%202/unnamed-chunk-7-1.png)

Question 2: A Hospital Audit
============================

For the first question, I am trying to logit regression model to figure
out the recall ratio for different radiologists. Using recall as
dependent variable, and added all else risk factors except cancer into
the model.

    ##              (Intercept) radiologistradiologist34 radiologistradiologist66 
    ##                   -3.275                   -0.522                    0.355 
    ## radiologistradiologist89 radiologistradiologist95               ageage5059 
    ##                    0.464                   -0.052                    0.111 
    ##               ageage6069             ageage70plus                  history 
    ##                    0.157                    0.108                    0.216 
    ##                 symptoms    menopausepostmenoNoHT menopausepostmenounknown 
    ##                    0.729                   -0.193                    0.403 
    ##         menopausepremeno          densitydensity2          densitydensity3 
    ##                    0.342                    1.220                    1.419 
    ##          densitydensity4 
    ##                    1.000

By using logit regression, I can interpret the parameter as partial
effects by holding all else fixed. Compare with radiologist13, which is
the baseline, the odds of recall for radiologist34 is e^(-0.522) times
of radiologist13, holding all else fixed. The odds of recall for
radiologist66 is e^(0.355) times of radiologist13, holding all else
fixed. The odds of recall for radiologist89 is e^(0.464) times of
radiologist13, holding all else fixed. The odds of recall for
radiologist95 is e^(-0.052) times of radiologist13, holding all else
fixed. Thus, radiologist89 has the highest probability of recall, which
means he/she is more conservative compare with others, holding all else
fixed.

For the second quesiton, as we know, the more variables we add into a
model, the higher the R-square ( the lower the in-sample square error).
Comparing model A with only recall as independent variable, and model B
with recall and all other risk variables. The coefficients from model B
shows that the radiologist were appropriately accounting for a patient’s
risk factor of breast cancer in interpreting the mammogram and deciding
whether to recall the patient for further screening. Also, the in-sample
RMSE is relatively smaller for B compare with A.

Coefficients for model A

    ## (Intercept)      recall 
    ##   -4.006120    2.260881

Coefficients for model B

    ##              (Intercept) radiologistradiologist34 radiologistradiologist66 
    ##             -5.475183784              0.019053992             -0.369522198 
    ## radiologistradiologist89 radiologistradiologist95                   recall 
    ##             -0.233148295             -0.384848670              2.335523469 
    ##               ageage5059               ageage6069             ageage70plus 
    ##              0.477892952              0.398328363              1.436442550 
    ##                  history                 symptoms    menopausepostmenoNoHT 
    ##              0.247483851             -0.008199087             -0.173097080 
    ## menopausepostmenounknown         menopausepremeno          densitydensity2 
    ##              0.819953395              0.230477972              0.718016350 
    ##          densitydensity3          densitydensity4 
    ##              0.834955961              1.998087115

In-sample RMSE of model A

    ## [1] 0.1936165

In-sample RMSE of model B

    ## [1] 0.1909821

However, when doing the out-sample prediction, model B does not show any
advantage than model A, instead, model B has higher out-of-sample RMSE.
Thus, it’s better to only consider recall when predicting cancer outcome
for new patients.

Out-of-sample RMSE (V1 for model A, V2 for model B)

    ##        V1        V2 
    ## 0.1904736 0.1942573

Question 3: Predicting When Artical Go Viral
============================================

After trying many different models, the best (with the smallest RMSE)
and interpretable model (easy to interpret the meaning of parameters)
for shares is using all artical-level features. The first model is doing
linear regression first and then threshold to get a confusion table,
corresponded error rate, true positive rate and false positive rate. The
result turns out to be a little bit wierd, with around 0.47 error rate,
high true positve rate but also high false positive rate.

Confusion table for the first model

    ##      viralhat
    ## viral    0    1
    ##     0  123 3878
    ##     1   41 3887

Error rate for the first model

    ## [1] 0.4942616

True Positve Rate for the first model

    ## [1] 0.9895621

False Positive Rate for the first model

    ## [1] 0.9692577

The second model is threshold first, and doing logit regression to get
prediction share. The result turns out to be better than the first
model, with smaller error rate, true positive rate and false positive
rate.

Confusion table for the second model

    ##      viralhat
    ## viral    0    1
    ##     0 2525 1475
    ##     1 1447 2482

Error rate for the second model

    ## [1] 0.3685206

True Positve Rate for the second model

    ## [1] 0.6317129

False Positive Rate for the second model

    ## [1] 0.36875

The reason why the results of these two models are quite different is
that, we can easily find the distrubution of shares has a very long
right tail by summarying variable shares.

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##       1     946    1400    3395    2800  843300

With high value outliner, it will distort (make it steeper) the linear
regression function. With first threshold shares, the outliners will
equal to one, which will be the same as other observations with shares
larger than 1400. Thus, the influence from outliner will be moved out
and make the model more accurate for prediction.
