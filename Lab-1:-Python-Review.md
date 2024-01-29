# Goal
The goal of this lab was to reviews important concepts in python while also reviewing general physics topics. We covered the concepts of python syntax, markdown, formatted printing, loops, conditionals, functions, and basic plotting.

# Overview

## Python Syntax
In this section, the main goal was to be able to read basic code cells. We needed to find the mistake within and fix it before running it again.
```python
from math import pi,cos

angle = pi/4.0

print(cos(angle))
```
This coded cell is an example of its corrected version. These cells had mistakes like missing parentheses or capitalization errors. This is important because the cells cannot run with spelling or punctuation errors.

## Markdowns
In this section, we learned some of the basic commands for Latex. Below is our example, for the symbols used to write out the text. In problem 1, we use "*" to first create bullet points, and then use one, two, or three side by side to help create the bold and/or italicized text. In problem 3, we use "$" at the beginning and end to help indicate an equation is being built. When a "\" is used, we are indicating a symbol is being used. The fraction command is represented by "\frac{}{}" where the first "{}" indicates the the numerator, while the second one indicates the denominator. Using the markdowns is important for creating titles and instructions. They can also be useful for writing equations and answers to future problems.
```latex
# 1.
*   **Here is the bold text.**
*   *Here is the italicized text*
*   ***Here is both the bold text and the italicized text***

# 3.
*   $v = v0 + at$
*   $\triangle x = (\frac{v+v0}{2})t$
*   $\triangle x = v0t + (\frac{1}{2})at^2$
```
## Formatted Printing
I found formatted printing very useful when printing out variables while producing a description along with it. We are able to print the results of a calculation, while also controlling the amount of significant figures. Below we can see that formatted printing always starts with 'f""' inside of the print function along with "{}" to withhold the variable we want printed. When a variable is followed by ":.2f", it means that we are calling for 2 decimal places. If we change the number, the amount of decimals places will correspond to the number that is chosen.
```python
print(f"my ratio = {myratio:.2f}")
```

## Loops
In the loops section, we learn how to utilize both sets of loops. For while loops, the function continues until the conditions are not met anymore. In for loops, we can use this function to iterate over lists automatically.
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
