# -*- coding: utf-8 -*-
"""
Created on Thu Jun 27 12:26:18 2019

@author: mtsco
"""
import numpy as np
from lmfit import minimize, Parameters
import scipy.integrate as spi
from scipy.optimize import leastsq
import matplotlib.pyplot as plt
from sympy import *
import xlrd

#x data
xdata = np.array([0.0, 0.0, 0.1, 0.1, 0.5, 0.5, 1.0, 1.0, 2.0, 2.0, 3.0, 3.0, 5.0, 5.0, 10.0, 10.0])
ydata = np.array([0.0 , 1, 1.2, 1.5, 3, 3.5, 6, 6.7, 10, 9.3, 20, 22, 30, 31, 36, 35.3 ])
errors = np.array([3, 0.4, 1, 2, 2.5, 3, 1.9, 1.9, 2.3, 1.8, 3.4, 4, 1.3, 2.4, 3.2])
ymax = np.amax(ydata)

def residual(params,x,y, stderrs):
#     f = lambda x, t : params['a']*x
    def f(x):
        #returning f(x), based on the current parameters
        #x is an array of all the x values
        a = (params['ymax'] * (x ** params['n'])) /\
                     (params['k'] + (x ** params['n']))
        import math
        for thing in a:
            if math.isnan(thing):
                print(a)
                print(thing)
                print("from a")
                print("\n\nymax: " + str(params['ymax']) + "\nn:  " + str(params['n']) +\
                      "\nk: " + str(params['k']))
                
        return (params['ymax'] * (x ** params['n'])) /\
                     (params['k'] + (x ** params['n']))
    
    #don't need this bc not an ODE
#    xsol = spi.odeint(f,[params['x0']],t)
    
    #my version
    yval = f(x)
    import math
    for thing in yval:
        if math.isnan(thing):
            print(yval)
            print(thing)
            print("from yval")
    
    errs = [ (a - b)/e for a,b,e in zip(yval, y, stderrs)]
    for foo in errs:
        if math.isnan(thing):
            print(errs)
            print(foo)
            print("from errs")
    return errs

#depending on the data, need to go thru and refine the starting conditions
p = Parameters()
p.add('k', min = 0, value=1000)
p.add('n', min = 0, value=5)
p.add('ymax', min = 0, value=ymax)

result = minimize(residual,p,args=(xdata,ydata, errors))
result.params.pretty_print()

xvals = np.linspace(0,max(xdata),420)
plt.plot(xvals,(result.params['ymax'] * (xvals ** result.params['n'])) /\
                     (result.params['k'] + (xvals ** result.params['n'])))
#final_yvals = (result.params['ymax'] * (xvals ** result.params['n'])) /\
#                     (result.params['k'] + (xvals ** result.params['n']))
plt.scatter(xdata,ydata)

plt.title("ymax = %.2f $\pm$ %.2f\nk = %.2f $\pm$ %.2f\nn = %.2f $\pm$ %.2f" % (
    result.params['k'].value, result.params['k'].stderr,
    result.params['n'].value, result.params['k'].stderr,
    result.params['ymax'].value, result.params['ymax'].stderr
))
  
        
        
        
        
        
        
        
        
        
        