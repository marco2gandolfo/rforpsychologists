---
title: <center> <font size="+3"> My First R Stuff </font> </center>
subtitle: <center> <font size="+3">'A basic R tutorial for psychologists' </font> </center>
author: "Marco Gandolfo"
date: "2019-03-11"
pagetitle: R
output: 
  html_document:
    keep_md: true
---




# My first attempt to use R

R is a programming language for statistical computing, similar to other programming languages (like matlab). What are its advantages? Honestly the most obvious one for me is that I can go from a computer to the other without panicking about software licenses, drivers, spending two hours installing toolboxes. Moreover, there is a broad community out there (beyond psychologists, notably very selfish people that do not share much their resources) ready to have dumb questions and responses to them.

# R is a calculator first of all 


```r
2+2
```

```
[1] 4
```

```r
50*(54-13)/42-3
```

```
[1] 45.80952
```
Guess you are thinking, very cool but this is what everyone teaches you in any course of programming and it is boring. And my answer is yes, is damn boring, I tried hard to get rid of these basics that sometimes are just confusing if you want to use R for your data but I can't!

But let's try to go on quickly

# Create Variables

Data can be stored into variables, variables have arbitrary names (also funny ones). In R you can create variables using the "<-" also called assignment operator. You can also use "=" but since the "=" sign has a use in some other bits where the assignment operator does not work I would advice you to use the "<-"

Here an example:

```r
Pizza <- "Margherita" 
#a string

LuckyNumber <- 13 
#An integer

Pizze <- c("Margherita","Funghi","Capricciosa","Focaccia","Calzone") 
#A character vector
    
LuckyNumbers <- c(13,17) # a numeric vector
```

# What we can do with Variables?

Well first of all we can use them to calculate stuff for instance


```r
LuckyNumber + 7 
```

```
[1] 20
```

```r
#You can also add a constant (luckynumber) 
#to a vector LuckyNmbers
LuckyNumber + LuckyNumbers
```

```
[1] 26 30
```

```r
#Obviously you can also multiply or Divide

LuckyNumber * 50 + 10
```

```
[1] 660
```
# Dataframes or Matrices

In R and for data analysis we will have to have notions of what vectors are but also of matrices. in R these are called dataframes and differently from the matlab matrixes they can have nice colnames and rownames.
A Dataframe is a two-dimensional vector which can have names for rows and columns.
How do you create a dataframe?

    data.frame(x = seq(10,1), y = seq(1,10))

The code says: Make a dataframe with two column variables, x and y. X contains a sequence from 10 to 1 and a sequence from 1 to 10. We can assign this dataframe a name and recall it as much as we do with variables. Another crucial symbol for R base is the $ (cash matters, a lot)
Anytime you have dataframes you have basically few variables stored into columns, you can call them by attaching to the name of the df a dollar (see below)


```r
df <- data.frame(x = seq(10,1), y = seq(1,10))

#When you assign it you need to call it to see its result normally

df
```

```
    x  y
1  10  1
2   9  2
3   8  3
4   7  4
5   6  5
6   5  6
7   4  7
8   3  8
9   2  9
10  1 10
```

```r
df$x # call the x variable
```

```
 [1] 10  9  8  7  6  5  4  3  2  1
```

```r
df$y # call the y variable
```

```
 [1]  1  2  3  4  5  6  7  8  9 10
```

## Okay cool, but what we can do now with that? 
I know you might are thinking, I could do this in excel in 5 minutes, but what's the advantage?
First of all here we can easily Index stuff, call elements of vector or a dataframe using the
"[]" brackets. The first element indicates rows, the second columns


```r
Pizze[3] #in the case of a vector we call with square brackets the third element
```

```
[1] "Capricciosa"
```

```r
df[4,1] #in the case of a dataframe we call the 4th row of the first column (seq from 10 to 1)
```

```
[1] 7
```

```r
df[,2] #Or with "nothing"plus comma we can call all the rows of the second column only
```

```
 [1]  1  2  3  4  5  6  7  8  9 10
```

```r
#You can also be cool and embed a vector in the indexes

df[c(1:5),] #I want only the rows from 1 to 5 of my df and of course both columns
```

```
   x y
1 10 1
2  9 2
3  8 3
4  7 4
5  6 5
```
Indexing will become crucial if you will ever start using for loops and all that fancier computer stuff but I will show you later how squared brackets are useful to call single elements or elements that correspond to certain features 

# Functions

Of course in R there are functions you can apply to your nice variables and numbers. Many of them are embedded into specific packages (all for free, no hidden costs(yet)) but just to show you quickly a few:


```r
sum(5,4,3,1,2)
```

```
[1] 15
```

```r
sum(df[1,])
```

```
[1] 11
```

```r
sum(LuckyNumbers) #maybe they are even luckier?
```

```
[1] 30
```

```r
mean(df$x)
```

```
[1] 5.5
```

```r
mean(df$y)  #arguably this should be the same, right?
```

```
[1] 5.5
```
# Logics
A logic is anything that returns a TRUE of FALSE. Is important that you know that logics are called this way because the word will come in any googled thing about R
The most common logic operators, at least those that I know, are:

1. **"=="** means equal to
1. **"&"** means AND, returns TRUE when both conditions are met at the same time
1. **"|"** means OR, returns TRUE when one condition or the other are met
1. **">"** greater than
1. **"<"** smaller than
1. **"!="** not equal to

Logics will be very important for If statements.


```r
mean(df$x) & mean(df$y) > 0
```

```
[1] TRUE
```

```r
mean(df$x) & LuckyNumber <= 5.5
```

```
[1] FALSE
```

```r
mean(df$x) | LuckyNumber == 5.5
```

```
[1] TRUE
```

```r
mean(df$x) == LuckyNumber
```

```
[1] FALSE
```

# Read data in R

The functions for reading in data in R depend on what kind of file you have. The most common options are .csv, .txt, and an Excel file. Let's look at each one of those. 

These functions have many arguments that help you defining some parameters of the text you are about to read.

    read.table("~/myexperiments/myexperiment/mydata/data.txt", sep = "\t", header = TRUE)
    
With this command I am reading a text file in a specific path and with a specific name "data.txt". I am telling R that this file uses tab separator "sep = "\t" " and to read the first column as name of the variables of the data frame (set this to false if your columns do not have a name by default).
The command above uses a function to read the file but reading isn't enough if we mean to work with these data in R. We need to store it into a variable!

    Rawdata <- read.table("~/myexperiments/myexperiment/mydata/data.txt", sep = "\t", header = TRUE)
    
If the file you are aiming to read is a .csv then the function "read.csv" will do the job.

# A practical example


```r
#If you are on windows instead of / you can use double \\ 
#or just / (copying the path and inverting their orientation)
#dataset taken from the fantastic website of joeymorey credits to him!

menu <- read.csv("~/OneDrive/RCourse_Made_by_Me/manuals/menu.csv", sep = ",")
```

Now I will introduce you some functions and few ways to look and slice/filter this nice dataset


```r
#what is the structure of the dataset, this gives you few crucial informations about the levels of your #factors and the number of your variables

str(menu)
```

```
'data.frame':	260 obs. of  6 variables:
 $ Category: Factor w/ 9 levels "Beef & Pork",..: 3 3 3 3 3 3 3 3 3 3 ...
 $ Item    : Factor w/ 260 levels "1% Low Fat Milk Jug",..: 76 77 228 229 230 245 12 11 14 13 ...
 $ Oz      : num  4.8 4.8 3.9 5.7 5.7 6.5 5.3 5.8 5.4 5.9 ...
 $ Calories: int  300 250 370 450 400 430 460 520 410 470 ...
 $ Fat     : num  13 8 23 28 23 23 26 30 20 25 ...
 $ Sugars  : int  3 3 2 2 2 3 3 4 3 4 ...
```

```r
#view the first 6 rows (head) and the last 6 (tail)

head(menu)
```

```
   Category                             Item  Oz Calories Fat Sugars
1 Breakfast                     Egg McMuffin 4.8      300  13      3
2 Breakfast                Egg White Delight 4.8      250   8      3
3 Breakfast                 Sausage McMuffin 3.9      370  23      2
4 Breakfast        Sausage McMuffin with Egg 5.7      450  28      2
5 Breakfast Sausage McMuffin with Egg Whites 5.7      400  23      2
6 Breakfast             Steak & Egg McMuffin 6.5      430  23      3
```

```r
tail(menu)
```

```
              Category                                              Item
255 Smoothies & Shakes            McFlurry with M&M\x89۪s Candies (Snack)
256 Smoothies & Shakes                McFlurry with Oreo Cookies (Small)
257 Smoothies & Shakes               McFlurry with Oreo Cookies (Medium)
258 Smoothies & Shakes                McFlurry with Oreo Cookies (Snack)
259 Smoothies & Shakes McFlurry with Reese's Peanut Butter Cups (Medium)
260 Smoothies & Shakes  McFlurry with Reese's Peanut Butter Cups (Snack)
      Oz Calories Fat Sugars
255  7.3      430  15     59
256 10.1      510  17     64
257 13.4      690  23     85
258  6.7      340  11     43
259 14.2      810  32    103
260  7.1      410  16     51
```

```r
#if you want to see more than 6 
head(menu,10)
```

```
    Category                                                          Item
1  Breakfast                                                  Egg McMuffin
2  Breakfast                                             Egg White Delight
3  Breakfast                                              Sausage McMuffin
4  Breakfast                                     Sausage McMuffin with Egg
5  Breakfast                              Sausage McMuffin with Egg Whites
6  Breakfast                                          Steak & Egg McMuffin
7  Breakfast                 Bacon, Egg & Cheese Biscuit (Regular Biscuit)
8  Breakfast                   Bacon, Egg & Cheese Biscuit (Large Biscuit)
9  Breakfast Bacon, Egg & Cheese Biscuit with Egg Whites (Regular Biscuit)
10 Breakfast   Bacon, Egg & Cheese Biscuit with Egg Whites (Large Biscuit)
    Oz Calories Fat Sugars
1  4.8      300  13      3
2  4.8      250   8      3
3  3.9      370  23      2
4  5.7      450  28      2
5  5.7      400  23      2
6  6.5      430  23      3
7  5.3      460  26      3
8  5.8      520  30      4
9  5.4      410  20      3
10 5.9      470  25      4
```

# An applied example of indexing


```r
class(menu) #this returns the type of variable menu is, is a dataframe so it has rows and columns
```

```
[1] "data.frame"
```

```r
#I want to take the first 10 observations of the first 4 variables
menu[1:10,1:4]
```

```
    Category                                                          Item
1  Breakfast                                                  Egg McMuffin
2  Breakfast                                             Egg White Delight
3  Breakfast                                              Sausage McMuffin
4  Breakfast                                     Sausage McMuffin with Egg
5  Breakfast                              Sausage McMuffin with Egg Whites
6  Breakfast                                          Steak & Egg McMuffin
7  Breakfast                 Bacon, Egg & Cheese Biscuit (Regular Biscuit)
8  Breakfast                   Bacon, Egg & Cheese Biscuit (Large Biscuit)
9  Breakfast Bacon, Egg & Cheese Biscuit with Egg Whites (Regular Biscuit)
10 Breakfast   Bacon, Egg & Cheese Biscuit with Egg Whites (Large Biscuit)
    Oz Calories
1  4.8      300
2  4.8      250
3  3.9      370
4  5.7      450
5  5.7      400
6  6.5      430
7  5.3      460
8  5.8      520
9  5.4      410
10 5.9      470
```

```r
#I want to take the first 10 observations of all variables excluding the first three columns -c (see negative sign)
menu[1:10, -c(1,2,3)]
```

```
   Calories Fat Sugars
1       300  13      3
2       250   8      3
3       370  23      2
4       450  28      2
5       400  23      2
6       430  23      3
7       460  26      3
8       520  30      4
9       410  20      3
10      470  25      4
```

```r
#I want to take the first 30 observation of column 4 and 6. For this we need the syntax c() for #vectors

menu[1:10,c(4,6)]
```

```
   Calories Sugars
1       300      3
2       250      3
3       370      2
4       450      2
5       400      2
6       430      3
7       460      3
8       520      4
9       410      3
10      470      4
```

```r
#once we know what we want to select from the main dataframe we can assign it to a variable

selmenu <- menu[1:30,c(1,3,4,6)]
```

Very cool, but sometimes, especially with bigger dataframes, to slice your dataframe you don't want to rely only on its position in the matrix. Could be quite confusing. Let's explore some other ways to do that in base R and let's start to have some more fun!


```r
#Hi base R, show me the first 6 lines in which the variable fat is == 0 excluding column one to 3

head(menu[menu$Fat == 0,-c(1:3)])
```

```
    Calories Fat Sugars
101       20   0      2
102       15   0      3
111      140   0     39
112      200   0     55
113      280   0     76
114      100   0     28
```

```r
#show me those lines where fat is 0 and they are not beverages or coffees and teas and store them in a #variable

zerofat <- menu[menu$Fat ==  0 & menu$Category != "Beverages" & menu$Category != "Coffee & Tea",]
```

*Congratulations!* You arrived this far and you won an undressed side salad! :)

What have we learnt so far?

1. **Some very basic R language and syntax that will help us to understand further**

1. **To read a file into R**

1. **To view it and to slice it or filter it.**

Not bad but there is a long way to go still.

## Process and visualise data with the Tidyverse

As said a particular power of R is to be able to choose from many open-source packages to do stuff.
One of the most famous ensemble of packages for datascience is what is called the Tidyverse. This macro-package is not for analysis directly but for data wrangling data cleaning and visualisation.

Let's install it! The sintax is always the same what changes is the name of the packages,
remember that installing a package is not enough. To use it you need to load it as well. See commands below:

    install.packages("tidyverse")  #to install it


```r
#to load it
library(tidyverse)
```

What is great about it (besides that is widely used and that it has a lot of support online) is that it is very coherent and likes to have the data always organised in the same way for all the functions that it uses. A tidy dataframe is simply a dataframe in which every observation is in a Row and every variable is in a column. In a psychology example is a dataframe in which in each row there is a trial and in each column all the independent and dependent variables for instance:


```r
tidyme <- data.frame(Subj = rep(1:20, each = 250), condition = c(rep("Cong",each = 125), rep("Incong", each = 125)), rt = rep(rnorm(250), each = 20 ))

str(tidyme)
```

```
'data.frame':	5000 obs. of  3 variables:
 $ Subj     : int  1 1 1 1 1 1 1 1 1 1 ...
 $ condition: Factor w/ 2 levels "Cong","Incong": 1 1 1 1 1 1 1 1 1 1 ...
 $ rt       : num  0.0354 0.0354 0.0354 0.0354 0.0354 ...
```

```r
summary(tidyme)
```

```
      Subj        condition          rt          
 Min.   : 1.00   Cong  :2500   Min.   :-2.99904  
 1st Qu.: 5.75   Incong:2500   1st Qu.:-0.62525  
 Median :10.50                 Median : 0.11756  
 Mean   :10.50                 Mean   : 0.05997  
 3rd Qu.:15.25                 3rd Qu.: 0.77850  
 Max.   :20.00                 Max.   : 3.07383  
```

```r
#This is an example of how a tidy dataframe would look
knitr::kable(head(tidyme, 10))
```



 Subj  condition           rt
-----  ----------  ----------
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176
    1  Cong         0.0354176

We will start with some very basic examples of data visualisation and some correlations and ttests on our fancy menu dataset. But, most importantly, we will learn how to wrap the data, create new columns and use all this tidyverse functions (from its dplyr package) that allow you to group the data and to average stuff.
One thing at a time!!

Remember at this point of the tutorial you absolutely need to have the tidyverse ensemble of packages installed and loaded  if you haven't done it yet.

    library(tidyverse)

# Visualising data in ggplot first.

**ggplot2** is a very complex and powerful tool for data visualisation. Even if it is quite hard to use it can give you instant satisfaction by doing pretty graphs with few lines of code.
Let's get all the reward that it gives for now.
First of all its philosophy is relatively straightforward. the "ggplot()" function wants to know what is the dataframe from which we wanna make the graph and an "aes()" argument in which we define the x variable and the y (dependent measure usually) axes of the graph.
The "+" sign is crucial for ggplot2 language and is honestly very handy. You can add elements to your graph by simply adding a plus sign. Each element is expressed in a function and what I usually do is to add to the "ggplot(df,aes(x,y))" what is the geometry, the type of graph that I want to do: "ggplot(df,aes(x,y)) + geom_point() " The function geom point will do a nice scatterplot. 
I am done with the talking, remember the structure is pretty much always like this one, the rest is about making it prettier with many many functions as it can be 100% flexible in each feature you want to modify.


```r
head(menu) 
```

```
   Category                             Item  Oz Calories Fat Sugars
1 Breakfast                     Egg McMuffin 4.8      300  13      3
2 Breakfast                Egg White Delight 4.8      250   8      3
3 Breakfast                 Sausage McMuffin 3.9      370  23      2
4 Breakfast        Sausage McMuffin with Egg 5.7      450  28      2
5 Breakfast Sausage McMuffin with Egg Whites 5.7      400  23      2
6 Breakfast             Steak & Egg McMuffin 6.5      430  23      3
```

```r
##Let's say I want to have a look at the linear relationship (I guess!) between calories and ##fat

calories_vs_fat <- ggplot(menu, aes(Calories,Fat)) + geom_point() #super basic scatterplot

#but to see it you have to call it
calories_vs_fat
```

![](ciao_files/figure-html/my first plot-1.png)<!-- -->

```r
#now let's play a little bit to add elements(regression line for instance).Do it one at a time

caloriesPretty <- calories_vs_fat + #call the previous plot we did and start adding stuff
                  geom_smooth(method = lm, se = TRUE) + # add line
                  ggtitle("The higher the calories the more the fat") + #add a title
                  theme_classic(base_size = 18) + #add a nicer theme
                  coord_cartesian(ylim=c(0,60)) + #let me see only values from 0 to 60 on y
                  coord_cartesian(xlim = c(0,1200)) + #let me see only values until 1200 kcal
                  theme(legend.title = element_blank())  #remove legend title
caloriesPretty  
```

![](ciao_files/figure-html/my first plot-2.png)<!-- -->

```r
caloriesPretty + aes(color = Category) #a bit crowded, add a color to data point per category
```

![](ciao_files/figure-html/my first plot-3.png)<!-- -->

```r
#now let's check the pearson's R with the cor function. This takes argument x(Calories), #y(Fat) and method = "pearson" (in this case)

cor(menu$Calories, menu$Fat, method = "pearson") #return only the R value! pretty high!
```

```
[1] 0.9044092
```

```r
cor.test(menu$Calories, menu$Fat) #return pearson's R and significance of correlation
```

```

	Pearson's product-moment correlation

data:  menu$Calories and menu$Fat
t = 34.048, df = 258, p-value < 2.2e-16
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.8795250 0.9243604
sample estimates:
      cor 
0.9044092 
```
Nice, now let's try other geoms other types of graphs that might be useful to you.

1. **"geom_histogram"** Histogram

1. **"geom_point"**  Scatterplot

1. **"geom_boxplot"** Boxplot

1. **"geom_line"** LinePlot

1. **"geom_bar"** A Barplot


```r
#boxplot
ggplot(menu, aes(Category,Calories)) + geom_boxplot() +
                theme_classic(base_size = 12, base_family = "Times")
```

![](ciao_files/figure-html/more graphs-1.png)<!-- -->

```r
#histogram
ggplot(menu, aes(Calories)) + geom_histogram()
```

![](ciao_files/figure-html/more graphs-2.png)<!-- -->

```r
#line plot, not sure this is super appropriate but to have an idea of the graph type.
ggplot(menu, aes(Fat, Calories, color = Category  )) + 
              geom_line() +
              coord_cartesian(xlim=c(0,30))
```

![](ciao_files/figure-html/more graphs-3.png)<!-- -->

# Group your data and prepare them for the analyses

## Now is time to play with *realistic* data 

We want to start doing more serious stuff now. And for that we will need "real" data
What we will do?

1. **Average a matrix by participant by condition to make it ready for an ANOVA**

1. **Compute new variables from the existing ones**

1. **Filter Participants or certain observations out**

1. **Perform an ANOVA with the "ez" package**

We will take **FAKE** (randomly generated) data of an imaginary experiment which represent a nice mixed anova design.

We compare two different image categorisation experiments (1 with face pictures the other one with objects). Different participants participated to the two experiments.

In each experiments participants were stimulated either to a FaceArea or a ObjectArea Moreover in both experiments the image to judge was either congruent or incongruent with a symbolic cue.

**So this is a simple 2 (face/object experiment(Between)) x 2 (TMS site, facearea/objectarea) x 2 (congruent/incongruent image cue) **

What do we expect? In the face experiment we expect effects on RT (and maybe also on the congruency) when stimulating the face area (site of interest) but not for the object area (control site). In the Object experiment we expect the opposite, some effect on RT for the object area but not the face area. 

We know already that there are 4 people to exclude over 46, and we will have thus 21 people per experiment which went through two stimulation sites and 2 rt conditions (congruent, incongruent).

It smells like we are hoping for a three way interaction Experiment x Site x Congruency but also an interaction Experiment x Site would be cool to see a site and task specific general effect on RT regardless congruency.

Remember that these data are not real so what we hope or hypothesised would be better not to appear :)


```r
# Note to myself Subjects to exclude "P19","P01", "p58","p63"

data <- read.csv("~/OneDrive/RCourse_Made_by_Me/manuals/bootdata2.csv", sep = ",", header = TRUE)

#quick inspection to check if things are right

head(data, 10)
```

```
       X SubjID Site   Task Congruency        RT Acc
1  11247    p64  ffa object       cong  906.8283   0
2   9908    p59   lo object     incong  737.1026   0
3  13723    p72   lo object       cong  634.5864   0
4   4440    P16  ffa   face     incong  528.5841   1
5   4874    P17   lo   face       cong 1011.2421   0
6  12645    p68   lo object       cong 1124.3055   0
7   5755    P20  ffa   face       cong  882.6555   1
8   4104    P15  ffa   face       cong  731.4093   0
9  13762    p73  ffa object     incong  918.9980   1
10 13461    p72  ffa object       cong  989.9528   0
```

```r
glimpse(data) #dplyr function to check structure similar to str()
```

```
Observations: 14,352
Variables: 7
$ X          <int> 11247, 9908, 13723, 4440, 4874, 12645, 5755, 4104, 13…
$ SubjID     <fct> p64, p59, p72, P16, P17, p68, P20, P15, p73, p72, P09…
$ Site       <fct> ffa, lo, lo, ffa, lo, lo, ffa, ffa, ffa, ffa, lo, lo,…
$ Task       <fct> object, object, object, face, face, object, face, fac…
$ Congruency <fct> cong, incong, cong, incong, cong, cong, cong, cong, i…
$ RT         <dbl> 906.8283, 737.1026, 634.5864, 528.5841, 1011.2421, 11…
$ Acc        <int> 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0,…
```

```r
#Check with xtabs how many trials by subject by site participants went through
#Ideally this is all matched

head(xtabs(~data$SubjID + data$Site))
```

```
           data$Site
data$SubjID ffa  lo
        P01 156 156
        P02 156 156
        P03 156 156
        P04 156 156
        P05 156 156
        P06 156 156
```
Two simple basic things already bother me. The first is that we have a column x whic we do not need, the second one is that our experiment between factor is called "Task" and, for clarity, we will rename it.

From now on I will use some dplyr functions

1. **"%>%"** Not directly a dplyr function also known as PIPE (c'est ne pas un pipe) this function works like the plus in ggplot 2. Allows you to keep going with the operations on your data without the need of useless code typing. You will love it. You can type it with a shortcut in R studio "cmd + shift + m"  

1. **"select"** regards COLUMNS and you can pick those that you need

1. **"filter"** regards ROWS and is useful to exclude rows (conditions of a variable or participants)

1. **"mutate"** computes a new column based on operations on other columns 

1. **"rename"** renames a specific column, equivalent to base r colnames(data$Task) <- "Experiment"

1. **"group_by"** genius fantastic function to wrap up your dataframe, for instance by participant by condition and make it ready to compute things on each member of the group. So is a pre-requisite to be able to collapse by participant by condition

1. **"summarise"** goes with the group_by and once a sumple is grouped you are able to summarise those groups using any function, as mean by participant by condition for RT, mean accuracy etc..

Let's start one by one and will be simple!
Remember, I said that I am annoyed by a useless X first column and the name of the between factor which I wannt to be called Experiment


```r
dataclean <- data %>% 
             select(-X) %>%  #unselect the column X mind about the - sign before
             rename(Experiment = Task) %>% #rename as Experiment the variable Task
             filter(!SubjID %in% c("P19","P01","p58","p63"))
```

Let's take a short break before averaging for the analyses. Select and Rename are pretty clear. I created a new variable called dataclean in which I removed the X dirty useless variable and renamed as I wanted the Task variable into Experiment. Then I filtered and the syntax might be slightly more obscure. The "%in%" sign means "Include". The Exclamation mark means "!" NO!!!!
So I am telling the function to keep All the Rows which Have a subject ID value that DO NOT contains "P19", "P01", "p58", "p63".

Now I think we are ready to generate a matrix in which we have mean Accurate RT mean accuracy by participant by condition. We will also use the mutate function to create a new column which in cognitive psychology is defined as "Efficiency". ReactionTimes/MeanAccuracy. So we give a cost in RT to those people that have been really accurate and a little discount to those that have been less accurate but very fast.

Let's do IT!


```r
AveMat <- dataclean %>% 
          group_by(SubjID, Experiment, Site, Congruency) %>%  #conditions to average for..
          summarise(meanRT = mean(RT[Acc==1]), meanAcc = mean(Acc)) %>% #apply function to ave
          mutate(Efficiency = meanRT/meanAcc)
```
Done!

We grouped by the conditions we wanted to do operations independently. In Each participant, in each experiment in each site in each RT condition we summarised to apply the mean function on RT (only accurate Trials) and on accuracy. After that we made a new column that computes the efficiency by dividing these new variables. I explicitly wanted to include mutate in this flow to show you its power. We can compute new variables based on columns we have just created and not yet seen.

# Do a 2 x 2 x 2 factorial ANOVA

For the ANOVA I will use the commonly and nice used package EZ. To make more friendly its results to look at I will use the package psychReport.

Install them please

```    
install.packages("ez")
install.packages("psychReport")

```    
Now let's load them 


```r
library(ez)
library(psychReport)
```

The ez package has many functions and they all pretty much have the same structure. The ez functions want as argument:

1. the dataframe you want to do the ANOVA from (**remember** this dataframe must be always in the long, not in the wide format, as our AveMat is)
1. the wid or case identifier, a unique value per case or Subject (in our field is normally the subject variable)
1. within factor
1. between factor if any.

These are only the main arguments you can give to ezANOVA but there are more (where you specify, if needed, covariates, the type of sum of square).
If you want to explore this you can refer to the help of ez which are pretty well done I believe. To open the ezAnova help or any help for any function please type:

    ?ezANOVA
    
Another handy function I use from this package is **ezStats**. This returns a matrix with mean and standard deviation of each condition and it is useful to see what is the direction of our effects.

Let's start our analysis by studying the Efficiency variable. This will be our dependent variable, our wid argument will be the SubjID, our within arguments the Site and Congruency (Within factors) and our between factor will be Experiment.

I will also try in the code to use the *psychReport* package to show you a pretty table of your results. I will use the nice aovTable function that wants the name of the variable where you store the model as an argument. Remember that to make this your ez model must have the argument "return_aov" and "detailed" equal to **TRUE**


```r
#store my anova into a variable that I call EFF_Model
EFF_Model <- ezANOVA(AveMat, dv =.(Efficiency), wid = .(SubjID), within = .(Site,Congruency), between = .(Experiment), return_aov = TRUE, detailed = TRUE)

#use aovetable function to make a nice table stored in EFF_Modelpretty variable
EFF_Modelpretty <- aovTable(EFF_Model, numDigits = 4, dispAovTable = TRUE)
```

```
════════════════════════ ANOVA:EFF_Model ═══════════════════════
                     Effect DFn DFd       F      p p<.05    pes
                 Experiment   1  40  0.0136 0.9079   .91 0.0003
                       Site   1  40  0.5397 0.4669   .47 0.0133
                 Congruency   1  40 11.4802 0.0016    ** 0.2230
            Experiment:Site   1  40  0.1066 0.7457   .75 0.0027
      Experiment:Congruency   1  40  0.0039 0.9505   .95 0.0001
            Site:Congruency   1  40  0.4903 0.4878   .49 0.0121
 Experiment:Site:Congruency   1  40  0.0330 0.8567   .86 0.0008
────────────────────────────────────────────────────────────────
```

```r
#ezStats to show the means and sd of each condition
ezStats(AveMat, dv =.(Efficiency), wid = .(SubjID), within = .(Site,Congruency), between = .(Experiment))
```

```
  Experiment Site Congruency  N     Mean       SD     FLSD
1       face  ffa       cong 21 1681.792 130.7294 178.1867
2       face  ffa     incong 21 1889.892 375.3252 178.1867
3       face   lo       cong 21 1703.939 149.1910 178.1867
4       face   lo     incong 21 1834.283 355.1147 178.1867
5     object  ffa       cong 21 1699.944 178.4489 178.1867
6     object  ffa     incong 21 1885.894 363.5244 178.1867
7     object   lo       cong 21 1679.292 226.9356 178.1867
8     object   lo     incong 21 1819.530 480.9719 178.1867
```

Nice eh!

# A real barplot with means and errorbars
Now we want to do a proper plot and this time we will tell ggplot to do some statistics on the matrix that we have to make a nice barplot that represent the mean and error bars that represent the standard error from the mean. *Stat_summary* wants to know which geometry the stats will return, which function and on which axis this is applied. Also we add position "dodge" (relatice to the distance of the bars) and color "black" (to color the border of the bars in black) arguments to make it prettier. Note the **labs** argument useful to give a name to the labels.


```r
Effbar  <- ggplot(AveMat, aes(Site, Efficiency, fill = Congruency )) +
           stat_summary(geom = "bar", fun.y = mean, position = "dodge", color = "black") + 
           stat_summary(geom = "errorbar", fun.data = mean_se, position = position_dodge(.9),width = 0.2) + 
           labs(y = "Efficiency ms/Acc", x= "Stimulation site")
Effbar
```

![](ciao_files/figure-html/barplot-1.png)<!-- -->
Nice Plot, but we are not quite there, we have error bars we have colors we have cool stuff but not yet the experiment factor in. To show an additional factor I like to use the argument "facet_wrap(~factor)".
Let's try to add it together with a nice theme to make the graph look prettier. Remember, now that our graph is stored we can straight add a plus to add elements to our graph, very handy.


```r
Effbar + facet_grid(~Experiment) + 
        theme_classic(base_size = 18, base_family = "Times") +
        scale_fill_grey() +
        coord_cartesian(ylim = c(1250,2000))
```

![](ciao_files/figure-html/prettiergraph-1.png)<!-- -->

I think this is a pretty acceptable paper friendly graph. There are many other personalisations and themes to explore. I created sort of my own theme for graphs and has been a pain but you can fully personalise it. 
Another good way to try stuff is to install packages that have expanded the amount of themes you could find.
One of these is *ggtheme*.

# Do pairwise comparisons with a simple t test?


```r
#ttest on efficiency as a function of congruency effect in the ffa site in the face experiment

Effttest <- t.test(Efficiency ~ Congruency, data= AveMat, paired = TRUE, subset = Site =="ffa" & Experiment == "face")
#Call it
Effttest
```

```

	Paired t-test

data:  Efficiency by Congruency
t = -2.3259, df = 20, p-value = 0.03065
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -394.73237  -21.46785
sample estimates:
mean of the differences 
              -208.1001 
```

```r
#make it prettier with the tidy function of the package broom
library(broom)
tidy(Effttest)
```

```
# A tibble: 1 x 8
  estimate statistic p.value parameter conf.low conf.high method
     <dbl>     <dbl>   <dbl>     <dbl>    <dbl>     <dbl> <chr> 
1    -208.     -2.33  0.0307        20    -395.     -21.5 Paire…
# … with 1 more variable: alternative <chr>
```

```r
#ttest of congruency as afunction of congruency only in the object experiment
#note that here I used the "subset" argument to filter the data 

Effttest <- t.test(Efficiency ~ Congruency, data= AveMat, paired = TRUE, subset = Experiment == "object")
```
Now friends we are at the end of this tutorial and what I want to do is a thing that I believe is useful.

# Transform your matrix from long to wide and make it SPSS or other crap software ready.

I think this is useful, you can export a matrix and make it user friendly for other software.
For some obscure reason someone does not want you to analyse your data in R?
Do you want to double check in another software if you have done things right?

While I think this is useful I strongly encourage you to abandon licensed software for analyses. Especially **SPSS**.
If you feel you want to have a friendlier interface than R please use softwares like **jamovi** or **jasp**. I still believe that learning this eventually will give you more chances in the angry job market or anyway to expand your knowledge about the analyses that you run.
They are open source, new and well done. Here we will make matrices that would be happily accepted by these softwares.

We will try to use the **unite** function from *tidyr* (part of the tidyverse) to join in one column all the condition names into a column (for instance "ffa_congruent"). After that we will use the **spread** function to spread the efficiency values by condition.
Another package that does that beautifully is the *reshape2* package but I believe is best to keep consistency among packages.

After that we will use the "write.csv" function to write a csv and store it in our working directory.
write.csv gets two argumens here 
    
    write.csv(dataframe, "path we want to write the file to")


```r
wide_eff <- AveMat %>% #take the averaged matrix
            select(-meanRT, -meanAcc) %>% #remove for now the meanrt and mean Acc
            unite(Condition,  Site, Congruency) %>% #unite all the within factors in a column called "condition"
            spread(Condition, Efficiency)

head(wide_eff, 10)  #check if it looks right
```

```
# A tibble: 10 x 6
# Groups:   SubjID, Experiment [10]
   SubjID Experiment ffa_cong ffa_incong lo_cong lo_incong
   <fct>  <fct>         <dbl>      <dbl>   <dbl>     <dbl>
 1 P02    face          1591.      1723.   1799.     2701.
 2 P03    face          1834.      1951.   1600.     1915.
 3 P04    face          1988.      1591.   1837.     2300.
 4 P05    face          1836.      1794.   1649.     1669.
 5 P06    face          1649.      1806.   1772.     1525.
 6 P07    face          1729.      1400.   1615.     1385.
 7 P08    face          1867.      1923.   1777.     2390.
 8 P09    face          1570.      1968.   1590.     2099.
 9 P10    face          1557.      2176.   1666.     1729.
10 P12    face          1529.      1404.   1629.     1181.
```

```r
write.csv(wide_eff, "~/OneDrive/RCourse_Made_by_Me/manuals/wide_eff.csv")
```

# Transform matrix from wide to long 

Here we use the **"gather"** function to go back into a long format matrix. I give it 3 arguments:

1. The name of the collapsed column that indicate the conditions "here" conditions
1. The name of my dependent measure that has been gathered.
1. The name of the columns, preceded by a minus, which I do not want to gather.

After that I use the handy *"separate"* function where I give it the name of the column which I want to separate, the names (as characters) of the new columns I want to create and the name of the separator.


```r
long_eff <- wide_eff %>% 
            gather(condition, Efficiency, -SubjID, -Experiment) %>% 
            separate(condition, c("Site", "Congruency"), sep = "_")

head(long_eff)
```

```
# A tibble: 6 x 5
# Groups:   SubjID, Experiment [6]
  SubjID Experiment Site  Congruency Efficiency
  <fct>  <fct>      <chr> <chr>           <dbl>
1 P02    face       ffa   cong            1591.
2 P03    face       ffa   cong            1834.
3 P04    face       ffa   cong            1988.
4 P05    face       ffa   cong            1836.
5 P06    face       ffa   cong            1649.
6 P07    face       ffa   cong            1729.
```

# Thanks a lot for listening/reading and hope this will be useful for you. 


![My aim is to make you become like this guy in the image below chasing people to talk about how cool "R" is.](/Users/psp905/desktop/riscool.png)


