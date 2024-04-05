# Goals

The goal of this lab is to use the trapezoid method of integration using python code to calculate and model different situations. In this lab, we created our trapezoid function to estimate the area under the curve. We estimated the area of a half circle using $f(x) = y = \sqrt{r^2 + x^2}$ with r = 2 and compared our estimated value to our accepted value of $y = 0.5\pi r^2$. We also use the trapezoid function to calculate the integral of the Gaussian Distribution by using $f(x) = \frac{1}{\sqrt{2\pi}{\sigma}}e^-\frac{1}{2}\frac{x-x_d}{\sigma}^2$. This is important because we are able to determine the area under a bell curve that represents the mean and standard deviation distributions. We then use built-in python functions that perform the integration. This was important to learn because it showed us how accurate my estimated value compared to preset python functions that do the same calculations. Lastly, we use the Monte Carlo method to visualize points above and below the curve. The Monte Carlo method allows us to model random samples or estimate the probabilities of situations, in this case we made a code to plot 1000 random points and distribute them above and below the half circle using our circle function.

# Overview

### Trapezoid

The first step in the lab was to build a function that takes in both x and y arrays to integrate through the trapezoid method. The x-value must be a range of values because it uses the integral xmin to xmax. We return the area for each case which can also be written as f(x). For the trapezoid area, we use $trap = 0.5(y_2 - y_1)*(x_2 - x_1)$

```python
def trap(x,y):
  area = 0
  for i in range(1,len(x)):
    trapezoid_area = 0.5*(y[i]+y[i-1])*(x[i]-x[i-1])
    area += trapezoid_area
  return area
```

### Area Under Half Circle & Gaussian Distribution

Both sections were very similar in Part 2 and Part 3 of the lab. In Part 2, we call our trap function while also using our function for the area of the circle. We found that through the integration, the area under the circle was 6.27644 and then compared it to our expected value. Our expected value for area in comparison to our calculated value gave us a percent error of 11%.

```python
def mycircle(x,r=2):
  y = np.sqrt(r**2 - x**2)
  return y

x_values = np.linspace(-2,2,100)
y_values = mycircle(x_values,2)

circle_area = trap(x_values,y_values)
print(f'The area under the circle is {circle_area:.5f}')

known = 0.5*np.pi*(2**2)
perc_error = (known - circle_area)/(known)*100
print(f'{perc_error:.2f}')
```

After comparing our estimated value to our expected value, we change the number of divisions or steps to 1000 to see if that would have an effect on the accuracy of the integral. We learned that adding more steps gives less spacing in between each point, so the accuracy is greater. After changing the step size, our area became 6.28297 with a percent error of 0.003352.

In Part 3 of the lab, we use a similar format to integrate over the Gaussian Distribution. The code we created allows us to input xmin to xmax, while also using the mean and standard deviation. We are able to calculate the probability theory curve.  Below is the code we used:

```python
def mygauss(x,mean,sigma):
  gauss = (1/(sigma*np.sqrt(2*np.pi)))*np.exp(-0.5*((x-mean)/sigma)**2)
  return gauss

sigma = 1
mean = 0
```
We are able to find the probabilities from the first standard deviation to the third standard deviation. Once again, we use our trapezoid function to help calculate the total area below the curve and then compare it to our expected values. In this case, our expected value must be updated each time we add another deviation because the probability of being under the curve is greater. 

```python
int_gauss = np.linspace(-1,1,100) # this is -sigma to sigma
y_gauss = mygauss(int_gauss,mean,sigma)

area_gauss = trap(int_gauss,y_gauss)
print(f'{area_gauss:.5f}')

known2 = 0.682
perc_error3 = np.absolute(known2 - area_gauss)/(known2)*100
print(f'{perc_error3:.2f}')

int_gauss2 = np.linspace(-2*sigma,2*sigma,100)
y_gauss2 = mygauss(int_gauss2,mean,sigma)

area_gauss2 = trap(int_gauss2,y_gauss2)
print(f'{area_gauss2:.5f}')

known3 = 2*(0.136+0.341)
perc_error4 = np.absolute(known3 - area_gauss2)/(known3)*100
print(f'{perc_error4:.2f}')

int_gauss3 = np.linspace(-3*sigma,3*sigma,100) # while this is -3sigma to 3sigma (third deviation)
y_gauss3 = mygauss(int_gauss3,mean,sigma)

area_gauss3 = trap(int_gauss3,y_gauss3)
print(f'{area_gauss3:.5f}')

known4 = 2*(0.021+0.136+0.341) # must update and add all the expected percentages
perc_error5 = np.absolute(known4 - area_gauss3)/(known4)*100
print(f'{perc_error5:.2f}')
```

### Built-In Functions

For the built-in functions, we imported new modules to use the trapezoid method. Instead of using our functions above, we use the code below (```np.trapz```):

```python
from scipy.integrate import trapz

new_trap = np.trapz(y_values,x_values)
new_gauss_trap = np.trapz(y_gauss,int_gauss)
```

This is important because importing a module may be a more simple, but still accurate way of calculating the area under curves. It may also save times as well. After printing the values of my calculated values and the values calculated from the built-in functions, we see the values are still very similar.

Half Circle: Our result is 6.276436078403619 and the expected answer is 6.276436078403621
Gaussian Distribution: Our result is 0.6826730329991479 and the expected answer is 0.6826730329991482

# Figures

### Monte Carlo

In this section, we learn how to implement the Monte Carlo method, which allows us to take a random set of data to visualize a specific situation. This is important because many situations can be too complex to solve for, but having an accurate visualization helps greatly. In our case, we were asked to created a function that visualized our half circle with a black solid line. Any random data point that fell below the function was plotted blue, and anything above was to be plotted red. This allows us to use both of our circle and trapezoid functions.

```python

# your monte carlo function here
def mcintegrate(radius=1,num=1000,visualize=False):
  xrandom = np.random.uniform(-radius,radius,num)
  yrandom = np.random.uniform(0,radius,num)

  below = yrandom <= mycircle(xrandom,radius)
  above = yrandom > mycircle(xrandom,radius)

  circ_area = np.sum(below)/num * (2*radius**2)

  if visualize == True:
    plt.figure(figsize=(12,8))

    x = np.linspace(-radius,radius,100)
    plt.plot(x,mycircle(x),'k-',label='Half Circle')

    plt.scatter(xrandom[below],yrandom[below],color='blue',label='point below')
    plt.scatter(xrandom[above],yrandom[above],color='red',label='point above')

  return circ_area
```

```python
xdist = np.linspace(-2,2,100)
ydist = mycircle(xdist)

areadist = trap(xdist,ydist)
myint = mcintegrate(2,visualize=True)
```
This allowed us to calculate an area of 6.276436 while also creating the plot of:

![download-6](https://github.com/kobestenson/COMPPHYS/assets/156839835/536dc7d9-35b0-4d33-a84c-35005ff5e7ef)
