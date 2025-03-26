Examination: Mozquizto Lab 1:A+B+C
Perform the tasks by writing and running appropriate R-code while answering the questions in the
accompanying three Mozquizto-tests at quizms.maths.lth.se. These tests will also provide you
with the information marked [mzq] below.

1 Lab 1: Problem description
In order to assess the concentration levels of poisonous metals in the environment, Naturv ̊ardsverket
(Swedish Environmental Protection Agency) measures the levels of a number of different metals in
moss every five years. Since the largest sources of emission have disappeared (been banned) during the
later decades, the levels in nature are declining over time.

We have access to the measurements from a handfull of Swedish regions in the file Pb_all.rda.
Download the data file and save it in the subfolder Data in your RStudio project folder. Start the
RStudio project and create an R-script file, e.g., lab1.R, and save it in the subfolder R in your RStudio
project folder. Write and run the necessary R-code in the script file.

Start by adding a header comment and initiate the package collection tidyverse. Alternatively you
can use only the packages ggplot2 (for plotting) and dplyr (for data manipulation). Then load the
data and look at the summary:

#Lab1####
library(tidyverse)
load("Data/Pb_all.rda")
summary(Pb_all)

Start the Mozquizto-test Lab 1.A: Linear model in order to find out which region you should analyse.
Extract the data for your region (replace [mzq] as appropriate) and look at the summary and the first
few lines:
Pb_myregion <- filter(Pb_all, region == "[mzq]")
summary(Pb_myregion)
head(Pb_myregion)

The variable Pb is the measured concentration level of lead (Pb) in mg/kg dry weight, that is, the
amount of mg lead per kg dried moss. We are interested in how fast the lead concentration decreases.

2 Lab 1: Lead in moss — change over time
1.A Linear model
1.A(a). Plot Pb against year:
##1.A Linear model####
###1.A(a)####
ggplot(Pb_myregion, aes(x = year, y = Pb)) + geom_point()
Does the relationship look linear? Should it be linear?
1.A(b). The measurements started in 1975 and it would be more resonable to use that as a starting point
instead of year = 0. Replot the data using x = year - 1975 instead of x = year.
1.A(c). Ignore the non-linear appearance and fit a linear regression model Yi = β0 + β1xi + εi where
Y = Pb and x = I(year - 1975). The I() is necessary in order to use a function, ”-”
= ”subtraction”, that R could confuse with ”-” = ”leave this variable out”. Calculate the β-
estimates, their standard errors and 95 % confidence intervals.
1.A(d). What is the average concentration of lead in 1975, according to this model?
1.A(e). How does the concentration change over time, on average, according to this model?
1.A(f ). Use the model to calculate a 95 % confidence interval for the expected average lead concentra-
tion in the year [mzq]. Does it seem reasonable?
1.A(g). Use the model to calculate a 95 % prediction interval for observations of the lead concentration
in the year [mzq]. Does it seem reasonable?
1.A(h). Plot the data together with the fitted line, a 95 % confidence interval for the fitted line and a
95 % prediction interval for new observations. Does it look reasonable?
1.A(i). Calculate the residuals and plot them against the predicted values. As visual aides, add a hori-
zontal reference line at 0 and a moving average, + geom_smooth(). Any problems here?
1.A(j). Make a Q-Q-plot and a histogram for the residuals. Problems?

1.B Log-transformation
Continue with Mozquizto-test Lab 1.B: Log-transformation.
1.B(a). The concentration of lead, when there are no new additions, should decrease at a constant rate,
e.g., 10 % per year. What type of model would this indicate and what type of transformations
would be natural for Y and/or x?
1.B(b). Plot y = log(Pb) against x = year - 1975. Does this seem like a linear relationship?
1.B(c). Fit this log-transformed linear model and calculate the β-estimates, their standard errors and
95 % confidence intervals.
1.B(d). What is the average log-concentration of lead in 1975, according to this model?
Lab 1: Lead in moss — change over time 3
1.B(e). How does the log-concentration change over time, on average, according to this model?
1.B(f ). Use the model to calculate a 95 % confidence interval for the expected average log-lead concen-
tration in the year [mzq].
1.B(g). Use the model to calculate a 95 % prediction interval for the logarithm of an observation of the
lead concentration in the year [mzq].
1.B(h). Plot the log-transformed data together with the fitted line, 95 % confidence interval and predic-
tion interval. How does this look compared to 1.A(h)?
1.B(i). Calculate the residuals and plot them against the predicted log-values. Also make a Q-Q-plot
and a histogram. How do these look compared to 1.A(i) and 1.A(j)? Comment?

1.C Back to the original scale
Continue with Mozquizto-test Lab 1.C: Original scale.
1.C(a). Write down how the concentration of lead, Pb, develops over time, first as a function of the
β-parameters in the model in 1.B, and then as a function of a = eβ0 and b = eβ1 .
1.C(b). Calculate estimates of a and b together with 95 % confidence intervals.
1.C(c). How high was the average (or rather, median) concentration of lead in 1975, according to the
estimated model?
1.C(d). How fast is the rate of decrease in lead concentration, according to the estimated model?
1.C(e). Use the model to calculate a 95 % confidence interval for the expected median lead concentra-
tion in the year [mzq].
1.C(f ). Use the model to calculate a 95 % prediction interval for an observation of the lead concentra-
tion in the year [mzq].
1.C(g). Plot y = Pb against x = year - 1975 together with the fitted relationship, 95 % confidence
interval and prediction interval. How does this look compared to the model in 1.A(h)?
1.C(h). Redo the plot with x = year instead. You only need to change the x= in the aesthetics, every-
thing else can be the same (except the label on the x-axis)
