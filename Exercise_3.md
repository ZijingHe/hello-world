Question 1
----------

    ## lm(formula = Rent ~ green_rating + size + empl_gr + leasing_rate + 
    ##     stories + age + renovated + class_a + class_b + net + amenities + 
    ##     cd_total_07 + hd_total07 + Precipitation + Gas_Costs + Electricity_Costs + 
    ##     cluster_rent + size:cluster_rent + size:Precipitation + stories:cluster_rent + 
    ##     net:cd_total_07 + size:leasing_rate + green_rating:amenities + 
    ##     hd_total07:Precipitation + age:cluster_rent + age:class_b + 
    ##     age:class_a + leasing_rate:cluster_rent + cd_total_07:cluster_rent + 
    ##     Precipitation:Gas_Costs + renovated:Precipitation + age:Electricity_Costs + 
    ##     renovated:Gas_Costs + stories:renovated + size:renovated + 
    ##     size:cd_total_07 + stories:amenities + amenities:Precipitation + 
    ##     amenities:Gas_Costs + class_b:Precipitation + class_b:Electricity_Costs + 
    ##     class_a:cluster_rent + renovated:cluster_rent + renovated:hd_total07 + 
    ##     cd_total_07:Precipitation + class_a:amenities + amenities:hd_total07 + 
    ##     Electricity_Costs:cluster_rent + renovated:Electricity_Costs + 
    ##     renovated:cd_total_07 + age:cd_total_07 + age:renovated + 
    ##     amenities:cluster_rent + class_a:Precipitation + class_a:Electricity_Costs + 
    ##     empl_gr:class_b + stories:Gas_Costs + class_b:hd_total07 + 
    ##     leasing_rate:Precipitation + class_a:hd_total07 + stories:age + 
    ##     size:age + size:class_a + green_rating:age + size:Electricity_Costs + 
    ##     size:hd_total07 + stories:Electricity_Costs, data = green)

    ##                    (Intercept)                   green_rating 
    ##                  -3.084249e+01                   1.239214e+00 
    ##                           size                        empl_gr 
    ##                  -1.895825e-05                   1.046989e-01 
    ##                   leasing_rate                        stories 
    ##                  -6.277115e-02                  -6.461606e-02 
    ##                            age                      renovated 
    ##                   1.946895e-02                  -5.998079e+00 
    ##                        class_a                        class_b 
    ##                   2.116325e+01                   2.007981e+01 
    ##                            net                      amenities 
    ##                  -3.719374e+00                  -1.698119e-01 
    ##                    cd_total_07                     hd_total07 
    ##                   2.071035e-03                   2.497870e-03 
    ##                  Precipitation                      Gas_Costs 
    ##                   7.738041e-01                   5.106208e+02 
    ##              Electricity_Costs                   cluster_rent 
    ##                   2.472945e+02                   8.186226e-01 
    ##              size:cluster_rent             size:Precipitation 
    ##                   6.082174e-07                  -1.968606e-07 
    ##           stories:cluster_rent                net:cd_total_07 
    ##                  -4.902770e-03                   1.085562e-03 
    ##              size:leasing_rate         green_rating:amenities 
    ##                   9.781801e-08                  -2.078601e+00 
    ##       hd_total07:Precipitation               age:cluster_rent 
    ##                  -5.932347e-05                  -2.868601e-03 
    ##                    age:class_b                    age:class_a 
    ##                  -3.692964e-02                  -2.643982e-02 
    ##      leasing_rate:cluster_rent       cd_total_07:cluster_rent 
    ##                   1.612536e-03                  -4.135371e-05 
    ##        Precipitation:Gas_Costs        renovated:Precipitation 
    ##                  -2.743632e+01                   9.792677e-02 
    ##          age:Electricity_Costs            renovated:Gas_Costs 
    ##                   1.994184e+00                  -5.192464e+02 
    ##              stories:renovated                 size:renovated 
    ##                  -2.072031e-01                   7.359122e-06 
    ##               size:cd_total_07              stories:amenities 
    ##                  -1.750557e-09                   1.132272e-01 
    ##        amenities:Precipitation            amenities:Gas_Costs 
    ##                  -9.475577e-02                   4.617372e+02 
    ##          class_b:Precipitation      class_b:Electricity_Costs 
    ##                  -1.453556e-01                  -3.088666e+02 
    ##           class_a:cluster_rent         renovated:cluster_rent 
    ##                  -5.473208e-02                   7.634128e-02 
    ##           renovated:hd_total07      cd_total_07:Precipitation 
    ##                   6.174126e-04                  -4.557269e-05 
    ##              class_a:amenities           amenities:hd_total07 
    ##                  -1.048037e+00                  -3.681478e-04 
    ## Electricity_Costs:cluster_rent    renovated:Electricity_Costs 
    ##                   3.992794e+00                   1.233421e+02 
    ##          renovated:cd_total_07                age:cd_total_07 
    ##                   9.558937e-04                  -1.018630e-05 
    ##                  age:renovated         amenities:cluster_rent 
    ##                   1.587855e-02                  -4.109201e-02 
    ##          class_a:Precipitation      class_a:Electricity_Costs 
    ##                  -1.014317e-01                  -2.680635e+02 
    ##                empl_gr:class_b              stories:Gas_Costs 
    ##                  -7.534432e-02                   1.782246e+01 
    ##             class_b:hd_total07     leasing_rate:Precipitation 
    ##                  -6.815226e-04                   8.187387e-04 
    ##             class_a:hd_total07                    stories:age 
    ##                  -6.353208e-04                   2.471052e-03 
    ##                       size:age                   size:class_a 
    ##                  -1.132036e-07                  -6.216895e-06 
    ##               green_rating:age         size:Electricity_Costs 
    ##                   3.755383e-02                   4.299117e-04 
    ##                size:hd_total07      stories:Electricity_Costs 
    ##                   6.811377e-10                  -4.380302e+00

1.  I use green rating as indicator of green certified, which equals 1
    when building is either LEED or Energystar. To figure out the best
    predictive model, I use forward selection method, step selection and
    backward selection, then, choose the model with the smallest AIC.
    For backward selection, the final model does not include green rate;
    comparing AIC between forward model(AIC=34512.51) and step model
    (AIC=34407.55), step model should be the best one.

2.  With and without green certification will change the average rental
    income per square foot, holding all else fixed, by 1.24 - 2.08 x
    amenities, which means the effect depends on whether amenities is
    available on-site. Although, in the step predictive model, there are
    interactions between age and green rating, the magnitude is quite
    small.

3.  The effect is different for buildings with amenities on-site and
    without amenities. On average, the effect is larger for buildings
    without amenities. The difference is around 2.08 on average.

Question 2
----------

(1)
===

There is simultaneity problem, which causes endogeneity of police with
respect to crime rate. It is hard distinguish whether the change of
crime rate cause the change of police or the change of police cause the
change of crime rate. For example, high crime rates are likely to
increase marginal productivity of police. Places with an inordinate
amount of crime, therefore, tend to employ a large police force, even if
police reduce crime. Thus, simple linear regression by using data from
different cities will generate biased estimators.

(2)
===

They wanted a variable which is unrelated to crime, but causes the
change of police, and they found the terrorism alert level was a great
case. By law, since Washington, D.C., is likely to be a terrorism
target, when the terror alert level goes to orange, then extra police
are put on the Mall and other parts of Washington to protect against
terrorists. It has nothing to do with street crime or things like that.
From table 2 column 1, the coefficient on the alert level is
statistically significant at the 5 percent level and indicates that on
high-alert days, total crimes decrease by an average of seven crimes per
day, or approximately 6.6 percent. Also, they considered that it was
possible that tourists were less likely to visit Washington or to go out
on high-alert day, which mean there were going to be less victims on the
street. From table 2 column 2, they verify that high-alert levels are
not being confounded with tourism levels by including logged midday
Metro ridership directly in the regression.

(3)
===

They considered that it was possible that tourists were less likely to
visit Washington or to go out on high-alert day, which mean there were
going to be less victims on the street. To control metro ridership, they
can check the hypothesis that whether high-alert levels are confounded
with tourism levels or not.

(4)
===

Table 4 tests whether police increase in one district will
decrease/affect police presence in other districts. If so, they would
expect to see higher levels of crime in other districts during
high-alert periods. From table 4 column1, during periods of high alert,
crime in the National Mall area decreases by 2.62 crimes per day. Crime
also decreases in the other districts, by .571 crimes per day, but this
effect is not statistically significant. Conclusion: First, police
increase in one district does not decrease police presence in other
districts. Second, the difference between the first raw and the second
raw shows the difference-in-difference estimator that controls for all
common factors between the districts.
