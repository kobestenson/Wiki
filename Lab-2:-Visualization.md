# Goal
The goal of this lab was to introduce basic plotting and visualization functions. The main tool we focused on was matplotlib.

# Overview

## Modules
In this section, all we did was import new modules.
```python
import numpy as np
from matplotlib import pyplot as plt
from astropy.table import Table
# the following module is used to read in image files
from matplotlib import image
%matplotlib inline
```

## Modulo Operator
We were introduced to the modulo operator and what to expect when using it. This is a tool to return the remainders of a division. The below problem should return "0" to indicate that there is no remainder.
```python
10 % 2
```
We then practiced by creating a function that took in an integer, and printed wether the number was odd or even.
```python
def oddeven(n):
  if type(n) != int:
    print(f'Warning, the number you entered is not an integer: {n}')
  elif n % 2 == 0:
    print("Even steven")
  else:
    print("That's odd...")
```

## Reading in Data from a File
This section is important because you are able to take any file and pull data from it easily. Without the need to spend time writing down all the data, you can pull pieces out using certain code.
```python
!wget http://www-personal.umich.edu/~mejn/cp/data/stars.txt

!ls

star_data = np.loadtxt('stars.txt')
```
The "!wget" command allows us to download a dataset, "!ls" shows the contents of the directory, and "np.loadtxt" allows us read in the data.

## Displaying Images
This uses the process from above, 
### While
```python
starting_num = 0

while starting_num <= 10:
  print(f"num = {starting_num}")
  starting_num = starting_num + 2
```
### For
```python
for numbers in range(0,11,2):
  print(numbers)
```

## Conditionals
For our conditionals, we learned how to use if, elif, and else statements to demand specific outputs during the execution of the program. This allows us to test what each result would be for the conditions we set.
```python
x = 25 * 32
y = 17 * 49

if x > y:
    print("The product of 25*32 is larger.")
elif x < y:
    print("The product of 17*49 is larger.")
```


## Functions
Functions allow us to take an argument, and then return a value through the function we create. In this case, our function is called feet2miles, and our argument is feet. e are looking to return miles.
```python
feet=100

def feet2miles(feet):
    miles = feet / 5280
    return miles

m = feet2miles(5280)
print(m) # Should be 1

m = feet2miles(1)
print(m)

m = feet2miles(1000)
print(m)
```
# Important Figures
In our first figure, we were able to plot a problem where a person threw a ball from a height of 50 meters high. Our graphs are a representation of what this problem may look like graphically using the corresponding kinematics equations. 

## Kinematics Code
```python
y0=50
v = 15
g = 9.8

def height(t): # note: do not use the word time
    return y0 + v*t - 0.5*g*t**2

def velocity(t):
    return v - g*t

def acceleration(t):
    return -g*np.ones(len(t))

time_values = np.linspace(0, np.sqrt(2*50/9.8), 100)

height_values = height(time_values)
velocity_values = velocity(time_values)
acceleration_values = acceleration(time_values)
```
To graph these equations side by side, we can use the subplot feature as a better visual comparison of position, velocity, and the acceleration curves. 

<img width="996" alt="Screen Shot 2024-01-28 at 10 23 38 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/944001ed-a418-4811-bbc9-13977a7c666d">

## Sin(theta) and Cos(theta)
In the last section of the lab, we are expected to graph sine and cosine as a function of theta. We are also given the range of 0 to 2pi. In our code this is given by ```np.linspace``` which set the range by (lower limit, upper limit, # of samples within the intervals).
```python
theta = np.linspace(0, 2*np.pi, 100) # 0<=theta<=2pi
sin = np.sin(theta)
cos = np.cos(theta)

plt.subplot(2,1,1)
plt.plot(theta, sin, label='sin(theta)')
plt.title('Sine Graph')
plt.ylabel('sin(theta)')
plt.legend()

plt.subplot(2,1,2)
plt.plot(theta, cos, label='cos(theta)')
plt.title('Cosine Graph')
plt.xlabel('Theta (in radians)')
plt.ylabel('cos(theta)')
plt.legend()
```

<img width="579" alt="Screen Shot 2024-01-28 at 10 24 52 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/da4611f5-4a2a-4d98-b703-f6f40e2067a9">
