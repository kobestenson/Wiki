# Goals

In this lab, the goals were to collect data for the position of a mass oscillating on a spring as a function of time. To describe this motion, we used the general solution of:

### $x(t) = A cos(wt - phi)$

In the second part of the lab, we use the Euler method to model simple harmonic motion.

# Part 1

## Setup

Below is an image of our setup for our data collection of simple harmonic motion. We used the graphical analysis pro to record oscillations over the duration of 10 seconds.

## Upload Data

We used code from previous lectures to import our collected data into the notebook. 

```python
from google.colab import files

uploaded = files.upload()

for fn in uploaded.keys():
  print('User uploaded file "{name}" with length {length} bytes'.format(
      name=fn, length=len(uploaded[fn])))

# used astropy to read in your data file
from astropy.table import Table
data = Table.read("csv-export (2).csv")
```

![download-6](https://github.com/kobestenson/COMPPHYS/assets/156839835/7b68b492-1964-4fff-956b-fe454e84667f)


Once we uploaded the data, we read in the data set with the table, and then saved time and position data. We also used the data to created our analytical solution by taking the position at each time and subtracted in by the mean position.

## Visualize and Analyze

From our collected data and mean data, we graphed the original values vs time and below it is the analytical solution.

![download-5](https://github.com/kobestenson/COMPPHYS/assets/156839835/95040335-72af-4973-9783-acdbfb6cffd7)


## Analytical Solution Parameters

For omega ($w$), we use the equation $w = 2\pi / T$ with the period we previously measure. This allowed us to create a function that calculated the position of the SHO, allowing us to plot our analytical solution versus our data.

```python
def calculate(A, omega, phi, time):
  position = A*np.cos(omega*time-phi)
  return position
```
![download-4](https://github.com/kobestenson/COMPPHYS/assets/156839835/f4ad6c70-b53e-49c9-9606-e3356ae8a583)


In the last part of this section, we determined our spring constant (k), initial position ($x_0$), and initial velocity ($v_x0$) using the code below:

```python
m = 0.1
T = 1.275

k= m*omega**2
x0 = mean_pos[0]
v0 = (mean_pos[1]-mean_pos[0])/(time[1]-time[0])
```

# Part 2

## Euler Method

Just like previous labs, we create our functions for acceleration, initialize, and calculate but adjust them for SHO. We also redefined our function for our general solution from part 1. Below are the functions we defined to use for our graphical illustrations.

```python
def acceleration(k,m,dx):
  """
  description: calculate acceleration using Hooke's Law

  parameters: k,m,dx

  return: acceleration


  """
  # your code here
  a = -k/m*dx
  return a
```

```python
def initialize(x0,v0,tmax,dt):
  """
  description: initialize time, position, and velocity into empty arrays

  parameters: x0,v0,tmax,dt

  return: t, pos, vel


  """
  nsteps = int(tmax/dt)
  t = np.zeros(nsteps)
  pos = np.zeros(nsteps)
  vel = np.zeros(nsteps)

  pos[0] = x0
  vel[0] = v0

  return t, pos, vel
```

```python
def calculate(t,pos,vel,k,m,dt):
  """
  description: calculate the position and velocity using the Euler method for time

  parameters: t,pos,vel,k,m,dt,xeq=0

  return: t, pos, vel
  """

  # your code here
  omega = np.sqrt(k/m)
  phi = 0.35

  for i in range(1,len(t)):
    pos[i] = pos[i-1] + vel[i-1]*dt
    vel[i] = vel[i-1] + acceleration(k,m,pos[i-1]*dt)
    t[i] = t[i-1] + dt

  return t, pos, vel
```
In our main program, we call our functions and overplot our analytical function over our Euler method position versus time.

![download-7](https://github.com/kobestenson/COMPPHYS/assets/156839835/c5e1dfb6-022d-4a0e-8e83-a49b09122ea2)


## Conservation of Energy 

When looking at our plot of energy versus time graph, the Euler solution does not conserve energy because the total energy is not constant over time. The Euler method can be a good approach but adjustments may need to be made for it to be more accurate.

![download-8](https://github.com/kobestenson/COMPPHYS/assets/156839835/9e1a76b2-dc24-451b-8057-6f889e0399ad)


## Euler-Cromer Solution

For the Euler-Cromer method, we see that parts of the code are changed. This allows the Euler method to become more efficient and prove energy conservation, as seen below.

![download-9](https://github.com/kobestenson/COMPPHYS/assets/156839835/9daa86a0-33a7-45af-9bc8-ce1ba618e03f)

![download-10](https://github.com/kobestenson/COMPPHYS/assets/156839835/0f8bb6a4-98df-441b-b47c-9d19ba055f8a)

