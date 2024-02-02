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
This uses the process from above, and then uses ```python image.imread```
```python
!wget http://www.envisionarchitects.com/files/9615/5017/1251/Siena_Obs_3.jpg

myimage = image.imread("Siena_Obs_3.jpg")

plt.imshow(myimage)
```
<img width="552" alt="Screen Shot 2024-02-02 at 11 27 43 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/6af1d02a-dfc0-4fd5-988f-43379f4370cf">

We can also use files from google drive by:

```python
from google.colab import files
uploaded = files.upload()
```

## Fitting a Straight Line
This section is very important for graphing data. We are able to create best-fit lines to show the average slope and trends of the data.
```python
c = np.polyfit(x,y,1)

xline = np.linspace(xmin,xmax,100)
yline = np.polyval(c,xline)
```


## Histograms
```python
plt.figure(figsize=(8,6))

gauss_values = np.random.normal(size=100)
plt.hist(gauss_values,color='black')
print("average value = {:.2f}".format(np.mean(gauss_values)))
print("the STD = {:.2f}".format(np.std(gauss_values)))

plt.axvline(np.mean(gauss_values),color='red',label='Average') # added line at average

plt.axvline(np.mean(gauss_values)+np.std(gauss_values),color='green',label='Std') # average + std

plt.axvline(np.mean(gauss_values)-np.std(gauss_values),color='green',label='Std')# average - std
```
<img width="665" alt="Screen Shot 2024-02-02 at 11 37 32 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/90db0fe1-d158-49f6-a4c5-1341b17272b9">

# Important Figures
## HR Diagram Plot
This is an important representation of what to expect from graphing data that is collected from a file.
<img width="618" alt="Screen Shot 2024-02-02 at 11 40 17 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/acfc731a-7f64-461a-b7a0-58f19f8e9ea7">

## Polar Plot


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
