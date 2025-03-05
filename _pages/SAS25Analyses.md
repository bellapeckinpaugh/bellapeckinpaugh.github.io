# Model 1

## *(H1) High-risk offspring will have greater symptoms of depression*

    ## Linear mixed model fit by REML. t-tests use Satterthwaite's method [
    ## lmerModLmerTest]
    ## Formula: RCADS.MD ~ risk_dummy + Age_kid + sex_dummy + (1 | kID)
    ##    Data: long_data
    ## 
    ## REML criterion at convergence: 1143.7
    ## 
    ## Scaled residuals: 
    ##     Min      1Q  Median      3Q     Max 
    ## -2.2377 -0.4531 -0.1793  0.2974  3.1695 
    ## 
    ## Random effects:
    ##  Groups   Name        Variance Std.Dev.
    ##  kID      (Intercept) 5.312    2.305   
    ##  Residual             6.018    2.453   
    ## Number of obs: 225, groups:  kID, 100
    ## 
    ## Fixed effects:
    ##              Estimate Std. Error        df t value Pr(>|t|)   
    ## (Intercept)  -0.89225    1.01209 157.70906  -0.882  0.37934   
    ## risk_dummy    1.27676    0.51379 185.42947   2.485  0.01384 * 
    ## Age_kid       0.22128    0.07475 158.97098   2.960  0.00354 **
    ## sex_dummy     0.38017    0.58807  99.94236   0.646  0.51946   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Correlation of Fixed Effects:
    ##            (Intr) rsk_dm Age_kd
    ## risk_dummy -0.139              
    ## Age_kid    -0.881 -0.087       
    ## sex_dummy  -0.344 -0.030  0.050

# Model 2

## *(H2) High-risk offspring will have worse reappraisal habits and (H4; exploratory) age will moderate this relationship*

    ## Linear mixed model fit by REML. t-tests use Satterthwaite's method [
    ## lmerModLmerTest]
    ## Formula: ERQCA.R ~ as.factor(risk_dummy) * Age_kid + sex_dummy + (1 |      kID)
    ##    Data: long_data
    ## 
    ## REML criterion at convergence: 735.3
    ## 
    ## Scaled residuals: 
    ##      Min       1Q   Median       3Q      Max 
    ## -2.64411 -0.55640 -0.01926  0.61300  2.34349 
    ## 
    ## Random effects:
    ##  Groups   Name        Variance Std.Dev.
    ##  kID      (Intercept) 0.4186   0.647   
    ##  Residual             1.0114   1.006   
    ## Number of obs: 232, groups:  kID, 100
    ## 
    ## Fixed effects:
    ##                                 Estimate Std. Error        df t value Pr(>|t|)
    ## (Intercept)                      4.83082    0.42643 127.70630  11.329  < 2e-16
    ## as.factor(risk_dummy)1          -1.72273    0.64954 163.26217  -2.652  0.00878
    ## Age_kid                         -0.02003    0.03277 133.12627  -0.611  0.54202
    ## sex_dummy                        0.07303    0.19275  83.43060   0.379  0.70575
    ## as.factor(risk_dummy)1:Age_kid   0.11454    0.05113 166.48362   2.240  0.02639
    ##                                   
    ## (Intercept)                    ***
    ## as.factor(risk_dummy)1         ** 
    ## Age_kid                           
    ## sex_dummy                         
    ## as.factor(risk_dummy)1:Age_kid *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Correlation of Fixed Effects:
    ##             (Intr) as.(_)1 Age_kd sx_dmm
    ## as.fctr(_)1 -0.587                      
    ## Age_kid     -0.929  0.575               
    ## sex_dummy   -0.275  0.006   0.048       
    ## as.f(_)1:A_  0.575 -0.961  -0.615 -0.015

## High-risk offspring reported worse reappraisal habits than low-risk individuals up until 15 years of age.

![](/images/unnamed-chunk-4-1.png)
<br>

## The relationship between risk and reappraisal was significant up until age 12.

    ## Registered S3 methods overwritten by 'broom':
    ##   method            from  
    ##   tidy.glht         jtools
    ##   tidy.summary.glht jtools

![](/images/unnamed-chunk-5-1.png)

# Model 3

## *(H3) Worse reappraisal habits will predict greater depression symptoms and (H5; exploratory) age will moderate this relationship*

    ## Linear mixed model fit by REML. t-tests use Satterthwaite's method [
    ## lmerModLmerTest]
    ## Formula: RCADS.MD ~ Age_kid * ERQCA.R + sex_dummy + (1 | kID)
    ##    Data: long_data
    ## 
    ## REML criterion at convergence: 1641.2
    ## 
    ## Scaled residuals: 
    ##     Min      1Q  Median      3Q     Max 
    ## -2.4446 -0.5040 -0.1712  0.2543  4.4393 
    ## 
    ## Random effects:
    ##  Groups   Name        Variance Std.Dev.
    ##  kID      (Intercept) 2.906    1.705   
    ##  Residual             6.980    2.642   
    ## Number of obs: 324, groups:  kID, 132
    ## 
    ## Fixed effects:
    ##                  Estimate Std. Error        df t value Pr(>|t|)    
    ## (Intercept)      -5.33146    2.25681 318.69323  -2.362 0.018758 *  
    ## Age_kid           0.71252    0.19745 318.01502   3.609 0.000357 ***
    ## ERQCA.R           0.80362    0.47145 316.55552   1.705 0.089253 .  
    ## sex_dummy         0.42435    0.44403 147.14281   0.956 0.340807    
    ## Age_kid:ERQCA.R  -0.09022    0.04146 316.11131  -2.176 0.030312 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Correlation of Fixed Effects:
    ##             (Intr) Age_kd ERQCA. sx_dmm
    ## Age_kid     -0.949                     
    ## ERQCA.R     -0.943  0.911              
    ## sex_dummy   -0.094  0.003 -0.025       
    ## Ag_:ERQCA.R  0.902 -0.957 -0.953  0.008

## The relationship between reappraisal habits and depression symptoms was significant after age 12

![](/images/unnamed-chunk-7-1.png)

# Model 4

\##(H6; exploratory) Directionality of the effects are such that risk
will predict future depression symptoms and future ER difficulties

    ## 
    ## Call:
    ## lm(formula = RCADS.MD.T2 ~ RCADS.MD.T1 + as.factor(risk.T1) + 
    ##     Age.T2, data = lag_data)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.1252 -1.9636 -0.9288  1.2467  8.0334 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)           3.6716     1.4404   2.549 0.013619 *  
    ## RCADS.MD.T1           0.4182     0.1012   4.132 0.000124 ***
    ## as.factor(risk.T1)1   1.9239     0.8380   2.296 0.025514 *  
    ## Age.T2               -0.1550     0.1148  -1.351 0.182378    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 2.866 on 55 degrees of freedom
    ##   (46 observations deleted due to missingness)
    ## Multiple R-squared:  0.3582, Adjusted R-squared:  0.3232 
    ## F-statistic: 10.23 on 3 and 55 DF,  p-value: 1.868e-05

# Model 5

## (H6; exploratory) Directionality of the effects are such that risk will predict future depression symptoms and future ER difficulties

    ## 
    ## Call:
    ## lm(formula = ERQCA.R.T2 ~ ERQCA.R.T1 + as.factor(risk.T1) + Age.T2, 
    ##     data = lag_data)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -2.7137 -0.6212  0.1039  0.6108  2.2334 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)          3.73045    0.75709   4.927 8.29e-06 ***
    ## ERQCA.R.T1           0.18604    0.11012   1.689 0.096915 .  
    ## as.factor(risk.T1)1 -1.09882    0.30740  -3.575 0.000749 ***
    ## Age.T2               0.04345    0.04246   1.023 0.310667    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.09 on 54 degrees of freedom
    ##   (47 observations deleted due to missingness)
    ## Multiple R-squared:  0.2497, Adjusted R-squared:  0.208 
    ## F-statistic: 5.991 on 3 and 54 DF,  p-value: 0.001335
