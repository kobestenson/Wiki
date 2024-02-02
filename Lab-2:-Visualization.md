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
Below is an example taken from matplotlib.org. We used the code below to print a line plot and what the sine and cosine of theta would look like.
```python
r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r

fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rmax(2)
ax.set_rticks([0.5, 1, 1.5, 2])  # Less radial ticks
ax.set_rlabel_position(-22.5)  # Move radial labels away from plotted line
ax.grid(True)

ax.set_title("A line plot on a polar axis", va='bottom')
plt.show()
```
<img width="452" alt="Screen Shot 2024-02-02 at 11 43 57 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/7ac57efd-bb15-4989-bb9a-2893dcbc9388">

```python
theta = np.linspace(0,2*np.pi,200)
r = np.sin(theta)

fig, ax = plt.subplots(subplot_kw={'projection': 'polar'},figsize=(6,6))
ax.plot(theta, r, label='sin(theta)')

# enter code to plot cos(theta)
r_cos = np.cos(theta)
ax.plot(theta, r_cos, label='cos(theta)')

ax.set_rticks([0.25, .5, .75,1])  # Less radial ticks
ax.set_rlabel_position(-22.5)
ax.grid(True)

ax.legend()

plt.show()
```
<img width="544" alt="Screen Shot 2024-02-02 at 11 45 50 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/5820a730-532c-498c-92f5-87e22bfc45d1">

## Multipanel Plot
We have used the subplot feature in previous classes using the code:
```python
plt.subplot(2,2,1)
```
This is useful for plotting graphs side-by-side.
<img width="629" alt="Screen Shot 2024-02-02 at 11 48 16 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/dc1ccded-3a31-4231-8cf5-0138206e8273">

## 3D Plots
An important reminder for 3D plots is to keep the projection equal to '3d':
```python
ax = plt.axes(projection = '3d')
```
<img width="404" alt="Screen Shot 2024-02-02 at 11 50 07 AM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/35b73df0-f698-4f5e-9506-eae557eabe3f">
