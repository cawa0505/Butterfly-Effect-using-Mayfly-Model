from matplotlib import *
from numpy import *
import statsmodels.api as sm

#--------------------1. Is there a Butterfly Effect?--------------------#
def mayfly(x,b,t):
    "x initial function, b growth factor, t # of steps to run"
    for i in range(t):
        print x
        x=b*(1-x)*x
        plot(i,x,"r.", ms=10)
        title("Population proportion vs Time")
        xlabel("Year")
        ylabel("Population proportion")
        
def mayflyalt(x,b,t):
    "x initial function, b growth factor, t # of steps to run"
    for i in range(t):
        print x
        x=b*(1-x)*x
        plot(i,x, 'b.',alpha=0.5, ms=10)
        title("Population proportion vs Time")
        xlabel("Year")
        ylabel("Population proportion")

#--------------------Then we test 4 comparison groups.--------------------#
mayfly(0.4, 1.5, 40)
mayflyalt((0.4+10**(-2)), 1.5, 40)
xlim(0,15)

mayfly(0.4, 4, 40)
mayflyalt(0.4+10**(-2), 4, 40) 

mayfly(0.4, 4, 40)
mayflyalt(0.4+10**(-2), 4, 40)
xlim(4,11)

mayfly(0.4,3.5,40)
mayflyalt(0.4+10**(-1),3.5, 40)
ylim(-6,6)
xlim(-5,40)

#--------------------Ok there's a butterfly effect--------------------#

#--------------------2. Plot Natural Log of Separation against time--------------------#
x=0.4
b=4
t=40
sep = 10**-3
m = x
n = x+sep
results = [sep]
for i in range(t):
    n = b*(1-n)*n
    m = b*(1-m)*m
    s = abs(m-n)
    results.append(s)
    semilogy(results,'r.')
    title("Natural log of separation vs. Years")
    xlabel("Years")
    ylabel("Natural log of separation")
    vlines(4, 0.0001, 1)
    vlines(11, 0.0001, 1)
    annotate('Here!', xy=(5, 0.15))
print len(results)
print results

#--------------------3. Find Best Linear Fit (OLS)--------------------#
from math import log

xaxis=range(0,t+1)[4:12]
print xaxis
xbar=mean(xaxis)
print xbar

yraw = [log(num) for num in results[4:12]]
y=asarray(yraw)
print y
ybar=mean(y)
print ybar

xy=asarray(xaxis)*asarray(y)
print xy
xybar=mean(xy) #xybar is generated
print mean(xy)

xsquare=asarray(xaxis)**2
print xsquare
mean(xsquare)
xsquarebar=mean(xsquare)
print xsquarebar  #xsquarebar is generated

beta=(xybar-xbar*ybar)/((xsquarebar)-(xbar*xbar))
print beta
alpha=ybar-beta*xbar
print alpha
fittedyvalues=asarray(xaxis)*beta+alpha
print fittedyvalues

scatter(xaxis, y,alpha=0.3)
pylab.plot(xaxis, fittedyvalues, "r-", alpha=0.3, linewidth=4)
title("Natural log of separation vs. Years")
xlabel("Years")
ylabel("Natural log of separation")


#--------------------4. Find linear model using statsmodel.api--------------------#
X = sm.add_constant(xaxis)

model = sm.OLS(y, X)
fit = model.fit()
print fit.summary()

scatter(xaxis, y,alpha=0.3)
pylab.plot(xaxis, fit.fittedvalues)
pylab.plot(xaxis, fittedyvalues, "r-", alpha=0.3, linewidth=8)
title("Natural log of separation vs. Years")
xlabel("Years")
ylabel("Natural log of separation")

#--------------------5. Residual Plots--------------------#
residual=y-fittedyvalues
scatter(xaxis,residual, alpha=0.4)
xlim(-2,42)
xlabel("t year")
ylabel("Residuals")
title("Residual Plot 1")

residual2=y-fit.fittedvalues
scatter(xaxis,residual2, alpha=0.4)
xlim(-2,42)
xlabel("t year")
ylabel("Residuals")
title("Residual Plot 2")
