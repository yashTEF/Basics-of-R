# Basics-of-R
*Following are the topics that are going to be covered*
* Grouping of Expressions,loops and conditional execution
* Creating user defined functions
* Graphical Uses of R

## Grouping, Loops and Conditional Execution
R is an expression language in the sense that its only command type is a function or expressionwhich returns a result. 
Commands may be grouped together in braces,{expr_1;...;expr_m}, in which case the value of the group is the result of the last expression in the group evaluated.  Since such a group is also an expression it may, for example, be itself included in parentheses and used as part ofan even larger expression, and so on
### Control statements
The language has available a conditional construction of the form - 
```R
> if (expr_1) expr_2 else expr_3 
```
There is a vectorized version of the if/else construct, the  ifelse function.  This has theform ifelse (condition, a, b) and returns  a vector of  the same  length as condition,  with elementsa[i] if condition[i]is true, otherwiseb[i](wherea and b are recycled as necessary).

###  Repetitive execution:for loops,repeat and while
There is also a for loop construction which has the form
``` R
  > for (name in expr_1) expr_2
```
where name is the loop variable.expr1 is a vector expression, (often a sequence like1:20), andex pr2 is often a grouped expression with its sub-expressions written in terms of the dummy name.expr2 is repeatedly evaluated as  name ranges through the values in the vector result of expr1. 
An example of how for can be useful
``` R

> for (i in 1:10) {
print(i)
}
```
Also we can use a while loop as follows
``` R
> while (condition) expr
 ```
 The breaks tatement can be used to terminate any loop, possibly abnormally.  This is the only way to terminate repeat loops.The next statement can be used to discontinue one particular cycle and skip to the “next”.

## User Defined Functions in R
As we have seen informally along the way, the R language allows the user to create objects ofmodefunction.  These are true R functions that are stored in a special internal form and may be used in further expressions and so on.  In the process, the language gains enormously in power,convenience and elegance, and learning to write useful functions is one of the main ways to make your use of R comfortable and productive.
A function is defined by an assignment of the form
``` R
> twosam <- function(y1, y2)
{n1  <- length(y1);
n2  <- length(y2)
yb1 <- mean(y1); 
yb2 <- mean(y2)s1  <- var(y1); 
s2  <- var(y2)s <- ((n1-1)*s1 + (n2-1)*s2)/(n1+n2-2)
tst <- (yb1 - yb2)/sqrt(s*(1/n1 + 1/n2))tst}
```
With this function defined, you could perform two samplet-tests using a call such as
``` R
> tstat <- twosam(data$male, data$female); tstat
```

### Defining new binary operators
Had we given the bslash() function a different name, namely one of the form %anything% it could have been used as abinary operatorin expressions rather than in function form. Suppose,for example, we choose!for the internal character.  The function definition would then start as
``` R
> "%!%" <- function(X, y) { ... }
```
### Named arguments and defaults
Functions in R can be defined in multiple formats following are some ways - 
``` R
> ans <- fun1(d, df, TRUE, 20)
> ans <- fun1(d, df, graph=TRUE, limit=20)
> ans <- fun1(data=d, limit=20, graph=TRUE, data.frame=df)
```
### Scope
The symbols which occur in the body of a function can be divided into three classes; formal parameters, local variables and free variables.  The formal parameters of a function are thoseoccurring in the argument list of the function.  Their values are determined by the process ofbindingthe actual function arguments to the formal parameters.  Local variables are those whosevalues are determined by the evaluation of expressions in the body of the functions.  Variableswhich are not formal parameters or local variables are called free variables. Free variables become local variables if they are assigned to.  Consider the following function definition.
``` R
f <- function(x)  {y <- 2*x print(x) print(y) print(z)}
```
In this function,x is a formal parameter, y is a local variable and z is a free variable.In R the free variable bindings are resolved by first looking in the environment in which the function was created.  This is called lexical scope.  First we define a function called cube.
``` R 
cube <- function(n) {sq <- function() n*n
n*sq()
}
```
## Graphical Applications of R
Graphical facilities are an important and extremely versatile component of the R environment.It is possible to use the facilities to display a wide variety of statistical graphs and also to buildentirely new types of graph.
Plotting commands are divided into three basic groups:
* High-level plotting functions create a new plot on the graphics device, possibly with axes,labels, titles and so on.
* Low-levelplotting functions add more information to an existing plot, such as extra points,lines and labels.
* Interactive graphics functions allow you interactively add information to, or extract infor-mation from, an existing plot, using a pointing device such as a mouse.

High-level plotting functions are designed to generate a complete plot of the data passed as ar-guments to the function.  Where appropriate, axes, labels and titles are automatically generated(unless you request otherwise.)  High-level plotting commands always start a new plot, erasing the current plot if necessary.
### the plot() function
One of the most frequently used plotting functions in R is theplot()function.  This is agenericfunction:  the type of plot produced is dependent on the type orclassof the first argument.
```plot(x,y)```

```plot(xy)``` 
If x and y are vectors,
```plot(x,y)```

produces a scatterplot of y against x.  The same effect  can  be  produced  by  supplying  one  argument  (second  form)  as  either  a  list containing two elements xand y or a two-column matrix.

```plot(x)``` 

If x is a time series,  this produces a time-series plot.  If x is a numeric vector,  itproduces a plot of the values in the vector against their index in the vector.  If x is a complex vector, it produces a plot of imaginary versus real parts of the vectorelements.

```plot(f)```

```plot(f,y)``` 
f is a factor object,y is a numeric vector.  The first form generates a bar plot off;
the second form produces box plots of y for each level off
### Displaying Graphics
Other high-level graphics functions produce different types of plots.  Some examples are:
``` R
qqnorm(x)
qqline(x)
qqplot(x, y)
```
Distribution-comparison plots.  The first form plots the numeric vector x against the expected Normal order scores (a normal scores plot) and the second adds a straight line to such a plot by drawing a line through the distribution and data quartiles.The third form plots the quantiles ofxagainst those of y to compare their respective distributions.

``` R
hist(x) 
hist(x, nclass=n)
hist(x, breaks=b, ...)
```
Produces  a  histogram  of  the  numeric  vectorx.   A  sensible  number  of  classes  isusually chosen,  but  a recommendation  can be  given with  then class=argument.Alternatively, the breakpoints can be specified exactly with the breaks=argument.
### Arguments to high level plotting functions
There  are  a  number  of  arguments  which  may  be  passed  to  high-level  graphics  functions,  asfollows:
``` R
axes=FALSE
```
Suppresses  generation  of  axes—useful  for  adding  your  own  custom  axes  with  theaxis()function.  The default,axes=TRUE, means include axes.
``` R
log="x"
log="y"
log="xy"
```
Causes the x, y or both axes to be logarithmic.  This will work for many, but notall, types of plot.
``` R
type=
xlab =
ylab =
main = string
sub = string
```
The type= argument controls the type of plot produced
### Low Level Plotting Commands
Sometimes the high-level plotting functions don’t produce exactly the kind of plot you desire.In this case, low-level plotting commands can be used to add extra information (such as points,lines or text) to the current plot.
``` R
points(x, y)
lines(x, y)
text(x, y, labels)
abline(a, b)
abline(h = y)
abline(v = x)
abline(lm.obj)
legend(x, y, legend...)
legend(.., fill = v)
legend(... ,col =v)
legend(...., lty = w)
legend(..., lwd = d)
legend(..., pch = ch)
```
1) Adds points or connected lines to the current plot.plot()’stype=argument canalso  be  passed  to  these  functions  (and  defaults  to"p"forpoints()and"l"forlines().)
2) Add  text  to  a  plot  at  points  given  byx, y.   Normallylabelsis  an  integer  orcharacter vector in which caselabels[i]is plotted at point(x[i], y[i]).  The default is 1:length(x)
3) Adds  a  line  of  slopeband  interceptato  the  current  plot.h=ymay  be  used  tospecifyy-coordinates  for  the  heights  of  horizontal  lines  to  go  across  a  plot,  andv=xsimilarly for thex-coordinates for vertical lines.  Alsolm.objmay be list with acoefficientscomponent of length 2 (such as the result of model-fitting functions,)which are taken as an intercept and slope, in that order.
4) Adds a legend to the current plot at the specified position.  Plotting characters, linestyles, colors etc., are identified with the labels in the character vectorlegend.  Atleast one other argumentv(a vector the same length aslegend) with the corre-sponding values of the plotting unit must also be given, as follows:

