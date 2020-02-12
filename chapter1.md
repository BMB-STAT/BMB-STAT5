---
title: 'STAT5 - Hypothesis Testing 2'
description: 'Hypothesis testing in more detail'
free_preview: true
---

## One sample t test

```yaml
type: NormalExercise
key: b1eb285d60
lang: r
xp: 100
skills: 1
```

The **one sample t test** compares the mean of one sample to a particular value.

**Example: Are our students taller than average?**

The mean height of 19 year-old females in the WHO reference data is 163.1548 cm. You could use a one sample t test to compare a sample of this year's students to this mean value.

`@instructions`
The height of a sample of 20 female students in this age group was measured and placed in the vector `heights`.

Perform a one sample t test to compare the mean of `heights` to the population mean (`mu =`) of 163.15.

You need to use the `t.test()` function, and you need to give it the list of all the heights in the sample rather than just the sample mean.

`@hint`
You need to enter 2 arguments: the vector of heights and the population mean: `mu = 163.15`

`@pre_exercise_code`
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)

```

`@sample_code`
```{r}
# t test to compare heights to 163.15


```

`@solution`
```{r}
# t test to compare heights to 163.15
t.test(heights, mu = 163.15)

```

`@sct`
```{r}
test_function("t.test", args = c("x", "mu"))
```

---

## One sample t test (2)

```yaml
type: MultipleChoiceExercise
key: f15bb8f875
lang: r
xp: 50
skills: 1
```

Perform the t test again to compare `heights` to a population mean of 163.15.

Look at the output.

With a threshold of $\alpha = 0.05$ do you reject the null hypothesis?

`@possible_answers`
- yes
- no

`@hint`


`@pre_exercise_code`
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
```

`@sct`
```{r}
test_mc(correct = 1)
```

---

## Two sample t test

```yaml
type: NormalExercise
key: 04f47ebac9
lang: r
xp: 100
skills: 1
```

The **two sample t test** compares the means of two samples.

Say you want to test whether a new compound causes overweight mice to lose weight. You could treat 10 mice with the drug and compare them to 10 mice which were not treated with the drug (or better still treated with a placebo drug).

The weights of 10 mice for each cohort have been stored in `data1`. The data are arranged with the weights stored in the `weight` column and a `treatment` column containing either `control` or `drug`.

`@instructions`
First use a box plot to compare the weights grouped by treatment.

Tip: Remember to use the `~` symbol in your formula for the boxplot.

`@hint`
The `~` symbol means, 'is explained by' or 'described by'. So you want to plot `weight` described by `treatment`. You also need to tell boxplot that the data is stored in `data1`.

`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
```

`@sample_code`
```{r}
# Boxplot of weight grouped by treatment

```

`@solution`
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

```

`@sct`
```{r}
test_function("boxplot", args = c("formula", "data"))
```

---

## Two sample t test (2)

```yaml
type: MultipleChoiceExercise
key: 7706d7aba9
lang: r
xp: 50
skills: 1
```

Take a look at the boxplot (resize the panel if necessary).

Does it look like the drug-treated mice have lost weight compared to the control mice?

`@possible_answers`
- Yes
- No

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
boxplot(weight ~ treatment, data = data1)
```

`@sct`
```{r}
test_mc(correct = 1)
```

---

## Two sample t test (3)

```yaml
type: NormalExercise
key: 1bb567adc1
lang: r
xp: 100
skills: 1
```

Since it looks like there's an effect, let's do a formal hypothesis test to quantify this.

`@instructions`
Perform a two sample t test to compare the weights grouped by treatment option.

`@hint`
Since you are entering the same data in `t.test()` and `boxplot()` you can use exactly the same formula.

`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
boxplot(weight ~ treatment, data = data1)
```

`@sample_code`
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment


```

`@solution`
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment
t.test(weight ~ treatment, data = data1)

```

`@sct`
```{r}
test_function("t.test", args = c("formula", "data"))
```

---

## Two sample t test (4)

```yaml
type: MultipleChoiceExercise
key: e70c80f493
lang: r
xp: 50
skills: 1
```

Repeat the t test you just performed and look at the output.

(t test on `weight` grouped by `treatment` in `data1`)

This time with a threshold of $\alpha = 0.01$ do you reject the null hypothesis?

`@possible_answers`
- Yes
- No

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
# boxplot(weight ~ treatment, data = data1)
```

`@sct`
```{r}
test_mc(correct = 2)
```

---

## Dealing with variation between replicates

```yaml
type: NormalExercise
key: 028ac3286c
lang: r
xp: 100
skills: 1
```

Statistics can be used to distinguish an effect which is masked by random variation - in other words, to detect a signal over the background noise.

The dataframe `data2`, contains the results of an siRNA knockdown experiment. In this experiment, a cell line was transfected with either an siRNA targetting a gene of interest (gene A) or control siRNA. The expression level of gene B was measured and is in the `output` column. 6 replicates were performed on different days. Take a look at the data to see if knocking down gene A has an effect on the expression level of gene B.

`@instructions`
Plot a boxplot for the `output` column grouped by `treatment` for the data in `data2`.

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

`@sample_code`
```{r}
# Boxplot of output grouped by treatment

```

`@solution`
```{r}
# Boxplot of output grouped by day
boxplot(output ~ treatment, data = data2)

```

`@sct`
```{r}
test_function("boxplot", args = c("formula", "data"))
```

---

## Dealing with variation between replicates (2)

```yaml
type: MultipleChoiceExercise
key: 4fb9825166
lang: r
xp: 50
skills: 1
```

Take a look at the boxplot you just plotted.

Does it look like the siRNA has an effect on expression of gene B?

`@possible_answers`
- Yes, a large effect
- Yes, a small but clear effect
- Possibly, a small effect
- No, no clear effect

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
boxplot(output ~ treatment, data = data2)
```

`@sct`
```{r}
test_mc(correct = 3)
```

---

## Dealing with variation between replicates (3)

```yaml
type: NormalExercise
key: c1998ab6d2
lang: r
xp: 100
skills: 1
```

It looks like there may be an effect, but the effect is small relative to the dispersion of the data.

Perform a two sample t test to determine the likelihood of observing a result like this if there were no effect.

`@instructions`
Perform a two sample t test on `output` grouped by `treatment` from `data2`.

Look at the output, and note down the *p value*.

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

`@sample_code`
```{r}
# t test on output grouped by treatment

```

`@solution`
```{r}
# t test on output grouped by treatment
t.test(output ~ treatment, data = data2)

```

`@sct`
```{r}
ex() %>% check_function("t.test") %>% check_arg("formula") %>% check_equal()
```

---

## Dealing with variation between replicates (4)

```yaml
type: MultipleChoiceExercise
key: acf3acd269
lang: r
xp: 50
skills: 1
```

With $\alpha = 0.05$ do you reject the null hypothesis?

`@possible_answers`
- Yes
- No

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
test_mc(correct = 2)
```

---

## Looking at the data more closely

```yaml
type: NormalExercise
key: 77c5375f09
lang: r
xp: 100
skills: 1
```

You failed to reject the null hypothesis, but let's take a closer look at the data.

The trouble with boxplots is that they don't show the individual data points. By looking at the raw data, you may see a pattern that isn't apparent from summary statistics.

You can use the `plot()` function to plot individual data points grouped by `day` to see how much variation there was between replicates. However, if the grouping variable is a factor, R will produce a box plot. If you tell it to treat `day` as a numeric variable using `as.numeric(day)`, it will plot a scatter plot.

`@instructions`
Plot a scatter plot of `output` grouped by `day` from `data2`

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

`@sample_code`
```{r}
# Scatter plot of output grouped by day

```

`@solution`
```{r}
# Scatter plot of output grouped by day
plot(output ~ as.numeric(day), data = data2)
```

`@sct`
```{r}
test_function("plot", args = c("formula", "data"))
```

---

## Looking at the data (even) more closely

```yaml
type: NormalExercise
key: 660cefb3bd
lang: r
xp: 100
skills: 1
```

That's great, but it would be helpful to know which datapoint refers to which treatment.

You can easily do this by colouring the data points with the `col =` argument.

`@instructions`
Add in the `col = ` argument to colour the datapoints by `treatment`.

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

`@sample_code`
```{r}
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2)
```

`@solution`
```{r}
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2, col = treatment)

```

`@sct`
```{r}
test_function("plot", args = c("formula", "data"))
# test_function("plot", args = "col")
test_error()
```

---

## Dealing with variation between replicates (5)

```yaml
type: MultipleChoiceExercise
key: dee54eda39
lang: r
xp: 50
skills: 1
```

Look at the scatter plot and interpret what the data show.

Note: Black = control and Red = siRNA

`@possible_answers`
- Output is consistently higher in siRNA group
- Output is consistently higher in control group
- No consistent difference between siRNA  control groups

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2, col = treatment)
```

`@sct`
```{r}
test_mc(correct = 1)
```

---

## Paired t test

```yaml
type: NormalExercise
key: 1dd88f988a
lang: r
xp: 100
skills: 1
```

Although the expression level in the control group varies considerably between replicates, the siRNA treatment appears to have a consistent effect on expression. The trouble with the two sample t test is that it compares the *mean* of each group. In this case, the variation between replicates swamps the siRNA effect.

So how can you analyse the data so that the consistent effect is detected over the variation between replicates?

The paired t test can help because, as the name suggests, it analyses the data in pairs. Try adding the argument `paired = TRUE` to the t test to see how this affects the outcome.

`@instructions`
Perform a paired t test on `output` grouped by `treatment` in `data2`.

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))

```

`@sample_code`
```{r}
# Paired t test on output grouped by treatment

```

`@solution`
```{r}
# Paired t test on output grouped by treatment
t.test(output ~ treatment, data = data2, paired = T)
```

`@sct`
```{r}
test_function("t.test", args = c("formula", "data", "paired"))
```

---

## Paired t test (2)

```yaml
type: MultipleChoiceExercise
key: 869ab52c54
lang: r
xp: 50
skills: 1
```

Once the background variation is controlled for, the siRNA effect now has $p < 0.00005$

For the paired t test to work in R, the data must be arranged in the same order in each group. In this case, both the control and siRNA data are sorted by day.

The paired t test can be used when observations in one group can be paired with observations in the other group. This may be because the observations were performed on the same subject (eg. mouse or patient), or because they were performed at the same time. There needs to be some reason why an observation in one group is more closely related to one particular observation, than the other observations in the second group.

Which of the following would not be suitable for analysis with a paired t test:

`@possible_answers`
- Does caffeine affect reaction time? Reaction times were measured in 20 students before and after taking caffeine.
- Does this cohort score higher marks than the last cohort? Exam scores from this year's cohort are compared to the same exam scores from last year's cohort.
- Is there a difference between steps recorded by smartphone apps or dedicated pedometers? Over a 24 hour period, 100 students recorded their steps on both a smartphone app and a pedometer device. The results from each device were compared.
- Have our students improved over the year? End of year exam scores of a cohort of 2nd year students were compared to their 1st year exam scores.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
test_mc(correct = 2)
```

---

## Assumptions of the t test (1)

```yaml
type: MultipleChoiceExercise
key: 1a4c22d00a
lang: r
xp: 50
skills: 1
```

Hypothesis tests are based on certain assumptions about the data. If the data do not fit these assumptions, the probability calculations underlying the test are likely to be incorrect. This could increase the chance of false positive or false negative results with potentially serious consequences.

So it is important to check the assumptions of any test you perform.

**Assumption 1: Continuous independent variable and bivariate dependent variable**

That's a bit of a mouthful, but it simply means that the outcome variable needs to be continuous, and the experimental variable needs to be categorical. Because the t test can only compare two groups, there can only have two levels for the dependent variable - that's what bivariate means. The underlying data may have more than two levels, but you can only analyse them two at a time with a t test.

Which of the following analyses fulfills this first assumption:

`@possible_answers`
- Testing whether the genotype of transgenic mice (homozygous, heterozygous or wild type for mutation A) affects the blood glucose level.
- Testing whether diet in mice (normal diet vs 'Western' diet) affects the time spent on running on an exercise wheel.
- Testing whether the number of eggs consumed in a month affects the blood cholesterol level.
- Testing whether the number of eggs consumed in a month affects the probability of suffering from myocardial infarction (heart attack).

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
test_mc(correct = 2)
```

---

## Assumptions of the t test (2)

```yaml
type: NormalExercise
key: cd73744d94
lang: r
xp: 100
skills: 1
```

**Assumption 2: Normal distribution**

The t test assumes the underlying population has a normal distribution. Remember, that this refers to the population, rather than your sample. If your sample appears normally distributed, this is a good indication that the population is too.

The simplest way to assess normality, is to look at a histogram of the data.

`@instructions`
Draw a histogram of the `heights` data you used for the one sample t test.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
```

`@sample_code`
```{r}
# Histogram of heights

```

`@solution`
```{r}
# Histogram of heights
hist(heights)
```

`@sct`
```{r}
test_function("hist", args = "x")
```

---

## Assumptions of the t test (3)

```yaml
type: NormalExercise
key: e1591a53fc
lang: r
xp: 100
skills: 1
```

As you can see, the data appear to follow a roughly normal distribution, with most values clustered around the mean and fairly symmetrical tails.

A normal quantile-quantile plot (Q-Q plot) is slightly more complicated but gives a clearer indication. This compares the quantiles (another name for percentiles) of your data with the theoretical quantiles from a normal distribution.

If that sounds like gobbledygook, don't worry. All you have to do, is see how well the data fall along a straight line.

`@instructions`
Use the `qqnorm()` and `qqline()` functions to test whether the `heights` data appear normally distributed.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
hist(heights)
```

`@sample_code`
```{r}
# Normal Q-Q plot of heights


# Add line to Q-Q plot of heights

```

`@solution`
```{r}
# Normal Q-Q plot of heights
qqnorm(heights)

# Add line to Q-Q plot of heights
qqline(heights)

```

`@sct`
```{r}
test_function("qqnorm", args = "y")
test_function("qqline", args = "y")
```

---

## Assumptions of the t test (4)

```yaml
type: NormalExercise
key: 73bcc6232e
lang: r
xp: 100
skills: 1
```

**Assumption 3: Equal variance**

The t test *usually* assumes that the two populations from which the samples have been taken have equal variance. In other words, the spread or dispersion of the values should be similar. You can check this by looking at the variance using summary statistics. (You could also check the standard deviation, since this is just the square root of the variance.)

*Actually* by default R uses the Welch's t test, which does not assume equal variance. If you are confident that the variance of your two samples are equal, you can specify this with argument `var.equal = TRUE`. This will increase the power of the test a little, but is most situations there's little advantage.

`@instructions`


`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
# boxplot(weight ~ treatment, data = data1)
```

`@sample_code`
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - unequal variance test
t.test(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - equal variance test

```

`@solution`
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - unequal variance test
t.test(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - equal variance test
t.test(weight ~ treatment, data = data1, var.equal=TRUE)
```

`@sct`
```{r}

```

---

## ANOVA

```yaml
type: TabExercise
key: 33023510c1
xp: 100
```

So far, we’ve looked at how we can compare data from two groups. Let’s imagine we are conducting a 3-arm trial where we have 3 groups A, B, C. We want to assess the differences among these groups (A vs. B vs. C).
How can we do it?
It would be inefficient to use two sample t-tests for A vs. B and A vs. C. etc. What can be used instead, when more than 2 independent groups are compared, is the one-way analysis of variance (ANOVA).
As you would expect, ANOVA with only 2 groups is identical to a two-sample t-test.

To run an ANOVA analysis similarly to t-test the following assumptions need to be satisfied:

1.	Data needs to be normally distributed
2.	Data should be from independent observations, which means that there is no relationship between the observations in each group or between the groups themselves.
3.	Equal variances between groups (Homogeneity of variances,Homoscedasticity)

Let’s look at an example.

`@pre_exercise_code`
```{r}
#insert some data here 
walk <- data.frame(subject = 1:45, speed = c(1.4,1.2,1.3,1.3,1.4,1.4,1.3,1.5,1.3,1.2,1.3,1.4,1.4,1.3,1.3,0.94,0.95,0.97,0.95,0.95,0.94,0.97,0.96,0.94,0.94,0.97,1.1,1.2,1.12,1.1,1,1.27,1.4,1.00,0.98,1,1.2,1.08,1.00,1,1.07,1.29,1.18,1.08,1.27), treatment = c(rep("control", 15),rep("water", 15),rep("land", 15)))
#ANOVA1 for use later
ANOVA1 <- aov(walk$speed~walk$treatment)
#data1 for use later
a<-c(3,5,6,7)
b<-c(7,8,10,11)
c<-c(4,4,5,6)
data1=data.frame(a,b,c)
```

***

```yaml
type: NormalExercise
key: a7f08e629d
xp: 15
```

`@instructions`
We want to assess the walking speed among 3 population groups categorised by the treatment received following a knee injury.

Look at the dataset named `walk`. 
If you look at the data, you see that you have 2 columns: one column contains walking speed values (numerical values) and the second column the corresponding groups. These are categorical values. The categorical values dictate how to group your data.

We want to test the following null hypothesis:
 
H0: The mean walking speed is the same in all three groups

Control = healthy controls<br />
Water = injured patients after receiving water-based physiotherapy<br />
Land = injured patients after receiving land-based physiotherapy <br />

Create a box plot of the data based on the treatment groups.

`@hint`
Remember, when you plot a boxplot, you need to define the dataframe and the groups you want to separate the data into.

`@sample_code`
```{r}
#create a boxplot of walk by treatment groups

```

`@solution`
```{r}
#create a boxplot of walk by treatment groups
boxplot(speed ~ treatment, data=walk)
```

`@sct`
```{r}
ex() %>% check_function("boxplot") %>% check_arg("formula") %>% check_equal()
```

***

```yaml
type: NormalExercise
key: a6f5476d83
xp: 15
```

`@instructions`
From the box plot you could qualitatively appreciate the differences between groups. Let’s now formally assess if the walking speed changes based on treatment received by running an ANOVA analysis.

In R ANOVA is run by using the `aov()` function. To visualise the output of the analysis the function `summary()` is used.

Tip: the results of the ‘aov’ function needs to be assigned to a new variable (e.g.:`ANOVA1<-`…) and you use the `~` symbol to group values according to the category they belong to.

`@hint`
Remember, aov needs to work on data (for example speed) and you need to indicate how the data should be grouped (for example treatment).

`@sample_code`
```{r}
#perform ANOVA using the function aov(data~category) and assign the output to variable 'ANOVA1'

#output the summary

```

`@solution`
```{r}
#perform ANOVA using the function aov(data~category) and assign the output to variable 'ANOVA1'
ANOVA1 <- aov(speed ~ treatment, data=walk)
#output the summary
summary(ANOVA1)
```

`@sct`
```{r}
ex() %>% check_function("aov") %>% check_arg("formula") %>% check_equal()
```

***

```yaml
type: MultipleChoiceExercise
key: ca7eaa76f7
xp: 15
```

`@question`
What R produces here is referred to as an ANOVA table. 
The first column represents the source of variation, both between groups (1st row - treatment) and within groups (second row - Residuals).
DF stands for degree of freedom. 

The degree of freedom (df) in statistics is equal to the values that are free to vary without changing the final calculation. 

You can think about in another way; if you know the mean of a dataset, you do not need to know all values within that dataset (n) - but n-1, as the last value can be calculated using the others. In this way, n-1 values in the dataset are free to vary without affecting the mean. 

The ANOVA compares the variance of different groups with each other. The number of different groups is known as m. So for example m could be the different kind of treatments or therapies in this case you are comparing with each other. 

Then we are also interested in the number of repeats or replicates which are labelled with the letter n. So in this case the walking speed of 15 patients were recorded for each group. 

Between groups DF is m-1, where m is the number of groups being compared. 

Within groups DF is n-m, where n is the total number of observations/data points collected. 

Choose the correct values of n and m.

`@possible_answers`
- m = 2, n = 42
- [m = 3, n = 45]
- m = 3, n = 42
- m = 2, n = 45

`@hint`


`@sct`
```{r}
# Check https://instructor-support.datacamp.com/en/articles/2375523-course-multiple-choice-with-console-exercises on how to write feedback messages for this exercise.
msg2 <- "Correct! there are 3 groups being compared, therefore m=3, and there are 45 datapoints collected, therefore n=45"
msg4 <- "This is incorrect - remember that m corresponds to the number of groups being compared, and n is the total number of data points"
msg1<-"This is incorrect - remember that m corresponds to the number of groups being compared, and n is the total number of data points"
msg3 <- "This is incorrect - remember that m corresponds to the number of groups being compared, and n is the total number of data points"

ex() %>% check_mc(2, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

***

```yaml
type: MultipleChoiceExercise
key: 3e143ae483
xp: 15
```

`@question`
Let’s continue to look at the table.
The third column is the Sum of Squares (quantifies variability between the groups of interest and within groups of interest in separate rows). 

The overall sum of squares is square of the difference between each datapoint and the overall mean, also called SST, for sum of squares (total).

Within the groups:

The sum of squares within the groups is defined as the square of the difference between each datapoint and the mean of the group it belongs to, also called SSW, for sum of squares (within). This shows the variation among each single groups. 

Between the groups:

The sum of squares within the groups is defined as the square of the difference between each mean of the groups and the overall mean for each datapoint, also called SSB, for sum of squares (between). This shows the variation among between the groups. 

From the ANOVA summary table, identify the correct values for the sum of squares (within) (SSW), and the sum of squares (between) (SSB). 

Remember, ANOVA represents between groups in the first row and within groups in the second row.

`@possible_answers`
- [SSB = 0.8539, SSW = 0.4535] 
- SSB = 2, SSW = 0.8539
- SSB = 42, SSW = 0.4535
- SSB = 0.4535, SSW = 0.8539

`@hint`


`@sct`
```{r}
# Check https://instructor-support.datacamp.com/en/articles/2375523-course-multiple-choice-with-console-exercises on how to write feedback messages for this exercise.
msg1 <- "Correct!"
msg4 <- "This is incorrect - remember, ANOVA represents between groups in the first row and within groups in the second row."
msg2<-"This is incorrect - remember, ANOVA represents between groups in the first row and within groups in the second row."
msg3 <- "This is incorrect - remember, ANOVA represents between groups in the first row and within groups in the second row."

ex() %>% check_mc(1, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

***

```yaml
type: MultipleChoiceExercise
key: c819d61196
```

`@question`
The fourth column is the Mean Squares (calculated by taking the Sum of Squares divided by DF on the same row). This is a variance estimate and what is used to calculate the F-statistic, the next column.
The fifth column is the F-statistic (calculated by Mean squares of row 1/mean squares of row 2). This is defined as the ratio between the Mean Squares between and within. 
These should sound familiar from STAT1, when we were calculating standard deviation. 
If this value is large then the chances are high that the variation between the group come from a statistically relevant effect, thus that the Null hypothesis can be rejected. Normally we would need to look up a threshold for the F value with a defined significance level, i.e. α = 0.05 in a table for the degrees of freedom we have here. If the value in the table is lower than we can reject the Null hypothesis.

However, R also calculates the p-value for us, so that we can just use it to make our decision.

From the p-value obtained, what can you conclude?

`@possible_answers`
- [Reject the null hypothesis]
- Fail to reject the null hypothesis

`@hint`


`@sct`
```{r}
# Check https://instructor-support.datacamp.com/en/articles/2375523-course-multiple-choice-with-console-exercises on how to write feedback messages for this exercise.
msg1 <- "Correct! You can see here that if we set our alpha at 0.05, the p value obtained from this analysis is less than 0.05, therefore we can reject the null hypothesis"
msg2 <- "This is incorrect - the p value is less than alpha, therefore we can reject the null hypothesis"


ex() %>% check_mc(1, feedback_msgs = c(msg1, msg2))
```

***

```yaml
type: MultipleChoiceExercise
key: 8e41b486fa
```

`@question`
In your reports or in other publication it is enough to report the most important output of the ANOVA test. It is common to report certain figures:

F(dfbetween, dfwithin) = Test Statistic, p =

What would be the most correct report of our ANOVA test?

`@possible_answers`
- There was a significant difference in mean walking speed (F(2,42) = 0.8543, 2.21e-10) within the groups.
- There was a significant difference in mean walking speed (F(3,45) = 39.54, 2.21e-10) between the groups.
- [There was a significant difference in mean walking speed (F(2, 42) = 39.54, p = 2.21e-10) between the groups.]

`@hint`


`@sct`
```{r}
# Check https://instructor-support.datacamp.com/en/articles/2375523-course-multiple-choice-with-console-exercises on how to write feedback messages for this exercise.
msg3 <- "Correct! This contains all the required elements in the correct place to report this result accurately"
msg1 <- "This is incorrect - the df values are correct, but check that you can correctly identify which is the test statistic."
msg2<-"This is incorrect - the test statistic is correct, but check that you can identify the degrees of freedom correctly."


ex() %>% check_mc(3, feedback_msgs = c(msg1, msg2, msg3))
```

***

```yaml
type: NormalExercise
key: 49c0e7e7bc
xp: 15
```

`@instructions`
Great! You now know how to run a one-way ANOVA analysis in R. 

From the p-value obtained we reject the null hypothesis meaning that there are differences between the groups’ means. The ANOVA analysis confirmed this but as it stands now, we do not know where those differences come from  - e.g.: group A different from B or is it B and C that are different? To determine where those differences exist, we need to run additional analyses: post-hoc tests.

A commonly used post-hoc tests is the Tukey Honest Significance tests. The R function is `TukeyHSD(fit)`, where `fit` is `aov(data~group)`.

Use a Tukey test on our walk data to find out where the differences are.

`@hint`


`@sample_code`
```{r}
#run a Tukey test using TukeyHSD()

```

`@solution`
```{r}
#run a Tukey test using TukeyHSD()
TukeyHSD(ANOVA1)
```

`@sct`
```{r}
ex() %>% check_function("TukeyHSD") %>% check_arg("x") %>% check_equal()
```

***

```yaml
type: MultipleChoiceExercise
key: 85c50c4ac2
xp: 15
```

`@question`
Take a look at the resulting table. The first column shows the differences between conditions, and the final column shows the adjusted p values.

We are interested in the last column where the p-values are reported. Since both p-values for the land and water treatment are below 0.05, we reject the null hypothesis, and we can state that they are significantly different from the healthy control group. However, there is no significant difference between the land or water walking treatments.

Moreover we can use for example the diff column, which shows the mean difference between each pair, to further explain/justify the results. The land physio group was 0.21 m/s slower than the control and the water physio was even slower.

Which is the most effective treatment to restore walking speed?

`@possible_answers`
- Water-based Physiotherapy
- Land-based Physiotherapy
- Both
- [None]

`@hint`


`@sct`
```{r}
msg1 <- "That's not quite right - although both comparisons are statistically significant, what does that actually mean for the interpretation of this experiment?" 
msg2 <- "That's not quite right - although both comparisons are statistically significant, what does that actually mean for the interpretation of this experiment?"
msg3 <- "That's not quite right - although both comparisons are statistically significant, what does that actually mean for the interpretation of this experiment?"
msg4 <- "That's correct - both comparisons between control and treatment are significantly different, therefore neither treatment has sufficiently improved walking speed"
ex() %>% check_mc(4, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

***

```yaml
type: NormalExercise
key: 27404e8dff
xp: 10
```

`@instructions`
To run ANOVA in R, data need to be in the same format as the one provided in the example. 

If the data are not in that format you can either use the function ‘stack’ to stack the vectors of your data frame one after another or step by step as shown in the following examples.

In the dataframe `data1` there are 3 groups to compare: a, b and c. 

Print `data1` - you should notice that this is not the correct format to run ANOVA in R.

The function `stack` can be used to convert this into an appropriate format.

Use `stack` to convert `data` in this way, and print it to the screen to see the difference.

`@hint`


`@sample_code`
```{r}
#Example 1
#print data1

#use the function stack to create the desired data format and assign it stacked 

#print stacked

```

`@solution`
```{r}
#Example 1
#print data1
data1
#use the function stack to create the desired data format and assign it stacked 
stacked<-stack(data1)
#print stacked
stacked
```

`@sct`
```{r}
ex() %>% check_function("stack") %>% check_arg("x") %>% check_equal()
```
