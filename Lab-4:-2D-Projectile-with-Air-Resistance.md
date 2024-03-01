# Goals

The goal of this lab was to apply the Euler Method to a problem with 2D projectile air resistance. The code for this situation was more complex than that of the radioactive decay.

```python
x[i] = x[i-1] + vx[i-1]*dt
vx[i] = vx[i-1] + ax(input_parameters)*dt

y[i] = y[i-1] + vy[i-1]*dt
vy[i] = vy[i-1] + ay(input_parameters)*dt
```

# Projectile Motion

In this section, we were able to use our known values to solve for the initial velocity in the x and y direction. Our initial conditions were:

```python
m = 10 #mass of a cannon ball (kg)
r = 0.1 #radius of cannon ball
g = 9.8 #acceleration

theta0_deg = 30 #degrees
theta0 = np.radians(theta0_deg) #the conversion of degrees to radians

y0 = 100 #meters
x0 = 0 #meters
v0= 150 #m/s

dt = 0.1
```
To determine our initial velocity in the x and y directions, we used sine and cosine to determine each vector and saved them to their corresponding variables:
```python
v0x = v0*np.cos(theta0)
v0y = v0*np.sin(theta0)
```

### Air Resistance

The goal of this section was to calculate the coefficient of air resistance ($B_2$) for the cannonball using:

### $F_d = C \rho Av^2 = B_2v^2$

We then took the value we collected for $B_2$, and then used it as an input to our acceleration functions that we defined as:

```python
def accel_y(v,B2,m):
  g = 9.8
  if v < 0:
    a = -g + B2/m*v**2
  else:
    a = -g - B2/m*v**2
  return a

def accel_x(v,B2):
  if v < 0:
    a = B2*v**2
  else:
    a = -B2*v**2
  return a
```

Because of the effect of air resistance, we cannot use our estimate of tmax because it may be inaccurate. We must use the append function to loop items to the end of the list after each value is updated.

```python
def calculate(x0,y0,v0x,v0y,B2,m,dt):
  """Calculate the air resistance"""
  vx = [v0x]
  vy = [v0y]
  x = [x0]
  y = [y0]
  t = [0]
  i = 1

  while y[i-1] >= 0:
    y.append(y[i-1]+ vy[i-1]*dt)
    x.append(x[i-1] + vx[i-1]*dt)
    vy.append(vy[i-1] + accel_y(vy[i-1],B2,m)*dt)
    vx.append(vx[i-1] + accel_x(vx[i-1],B2)*dt)
    t.append(t[i-1]+dt)
    i = i+1

  return t, x, y, vx, vy
```
# Plots
Below is our plots for the returned values within our calculate function. We took our x and y positions/velocities and graphed them against time.
<img width="825" alt="Screen Shot 2024-03-01 at 12 39 51 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/4ef099cc-cc01-4fb4-8bf9-32ff9e919062">

We also created a plot to show the changes for each angle with air resistance still present:
```python
theta0_deg = np.arange(15,90,15)

for mytheta in theta0_deg:
  y0 = 100
  x0 = 0
  v0=150
  v0x = v0*np.cos(np.radians(mytheta))
  v0y = v0*np.sin(np.radians(mytheta))

  t, x, y, vx, vy = calculate(x0,y0,v0x,v0y,myB2,m,dt)

  plt.plot(x,y,label=r"theta = degrees".format(mytheta))
  plt.plot(np.linspace(-10,50,100),np.linspace(100,100,100),'k-',alpha=0.5) #creates the box
  plt.plot(np.linspace(50,50,100),np.linspace(-10,100,100),'k-',alpha=0.5) # ^^^
  plt.fill_between([-10,50],-10,100,color='lightgrey') #creates the fill in the box

plt.xlabel('X-position (m)')
plt.ylabel('Y-position (m)')
plt.title('Y-position vs X-position')
plt.legend()
```

<img width="627" alt="Screen Shot 2024-03-01 at 12 45 07 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/0e7a3033-c5a0-4cdd-b8cd-e7a6f7896321">

# Summary Questions

The initial angle affects the height and distance. Angles lower than 45 degrees product small heights and greater distances, angles higher than 45 created greater heights and smaller distances. 45 degrees creates the third highest elevation while also creating the longest distance. The range values with air resistance are shorter than the range without air resistance because the force of drag is opposite of velocity which would force the ball to slow down.