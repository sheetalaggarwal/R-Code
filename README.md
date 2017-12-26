# R-Code
#1.	Create a column for single mothers (gender = 0, married = 0, children = 1) and a second column for single fathers (gender = 0, married = 0, children >= 1).  Perform a regression using these two columns, as well as Salary and Catalogs to predict AmountSpent.  Are either of these new columns statistically significant in predicting AmountSpent?  Are they positively or negatively related?
#Solution:   columns single mother and single father are very less statistically significant when the children >=1 as the p value for both the columns are 0.0449 and 0.0307 respectively which is very near to 0.05 and both the columns have negative coefficients so they are negatively related.
#Code
       Catalog = read.csv(file.choose())
head(Catalog)
tail(Catalog)
Catalog$SingleMothers = ifelse(Catalog$Gender==0 & Catalog$Married==0 & Catalog$Children>=1 , 1 , 0)
Catalog$SingleFathers = ifelse(Catalog$Gender==1 & Catalog$Married==0 & Catalog$Children>=1 , 1 , 0)
head(Catalog)  
CatalogRegr = lm(AmountSpent ~ SingleMothers + SingleFathers + Salary + Catalogs , data = Catalog)
summary(CatalogRegr)
#Output: 
Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
(Intercept)   -5.748e+02  6.363e+01  -9.033   <2e-16 ***
SingleMothers -1.114e+02  5.545e+01  -2.008   0.0449 *  
SingleFathers -1.533e+02  7.085e+01  -2.164   0.0307 *  
Salary         1.916e-02  7.026e-04  27.268   <2e-16 ***
Catalogs       5.108e+01  2.918e+00  17.504   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 597.7 on 995 degrees of freedom
Multiple R-squared:  0.6148,	Adjusted R-squared:  0.6133 
F-statistic: 397.1 on 4 and 995 DF,  p-value: < 2.2e-16
