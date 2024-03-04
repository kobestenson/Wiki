# Goals

The goal of this lab is to model the motion of a planet orbiting a star. We start by modeling Earth around the Sun for a two body system.

# Functions

We take a different path for building functions and properly modeling the orbits. We used our typical initialize and calculate functions, while also adding in a distance function to measure between the Earth and the Sun. We also built a function to make plots.

```python
def make_plots(time,x,y,vx,vy):
  plt.figure(figsize=(15,4))
  plt.subplots_adjust(wspace=.35)

  plt.subplot(1,3,1)
  plt.title('Orbit')
  plt.scatter(x,y,c=time,s=10)
  plt.colorbar(label="Time (yr)")
  plt.axis('equal')

  plt.subplot(1,3,2)
  r = np.sqrt(x**2+y**2)
  plt.title('Position vs Time')
  plt.plot(time,x,label='xpos vs time')
  plt.plot(time,y,label='ypos vs time')
  plt.plot(time,r,label='radius vs time')
  plt.xlabel('Time (yr)')
  plt.ylabel('Distance (Au)')
  plt.legend(loc='lower left')

  plt.subplot(1,3,3)
  v = np.sqrt(vx**2+vy**2)
  plt.title('Velocity vs Time')
  plt.plot(time,vx,label='x-velocity vs time')
  plt.plot(time,vy,label='y-velocity vs time')
  plt.plot(time,v,label='V-magnitude vs time')
  plt.xlabel('Time (yr)')
  plt.ylabel('Velocity (Au/yr)')
  plt.legend(loc='lower right')
```

## Question 1
**Describe the Earth's orbit. How does the radius change with time? How does the magnitude of the velocity or speed change with time?**

From our graphs, it is evident that as time passes, Earth's orbit shows us that as x is furthest from 0, than y = 0, and vise versa. When the x-position is 0, is velocity is the greatest in the x-direction, when the y-position is 0, the y-velocity is the greatest.

![download-18](https://github.com/kobestenson/COMPPHYS/assets/156839835/9eeb0d04-3b0c-432b-b698-47e000281b77)


## Question 2, Modifying Initial Velocity

When velocity is increased, the orbit does change. We can see that when the radius between the two planets are the greatest, the velocity is smaller. This makes me believe that increasing velocity would cause the orbit to become more elliptical. When Earth is closest to the Sun, the velocity is always the greatest.

![download-16](https://github.com/kobestenson/COMPPHYS/assets/156839835/bb6dd499-0c1e-4764-8051-d12d2a8e83d3)


When the velocity is decreased, the orbit changes. Just like before, when the radius between the two planets are the greatest, the velocity is smaller. Speed is always the greatest when the Earth is closest to the Sun because of the gravitational force.

![download-17](https://github.com/kobestenson/COMPPHYS/assets/156839835/024602d3-ee2d-429f-88b7-36e1942a5655)


Our model is consistent with Kepler's 1st law because our models are consistent with that of an ellipse. We know when the orbit is elliptical because the velocity is not constant the entire time, if the velocity was constant the orbit would be a circle.

Kepler's 2nd is modeled in the graphs because velocity changes for each position the Earth reaches.

## Question 3

The orbit does stay stable because point on the orbit overlap. We also see no changes on the position and velocity graphs. Below are the illustrations of a total time (in years) of 2, 3, and 4.

![download-15](https://github.com/kobestenson/COMPPHYS/assets/156839835/b32a36ee-83db-4ad1-95b3-17a4551ce745)


![download-14](https://github.com/kobestenson/COMPPHYS/assets/156839835/97070fda-9814-4e2c-9b26-f6290b662a07)


![download-13](https://github.com/kobestenson/COMPPHYS/assets/156839835/c40add54-a9cb-4067-b1fd-8d24b9473c44)


## Question 4, Euler vs Euler-Cromer Method

The orbit does not stay stable using the Euler method, we can see a spiral on the graph. The radius begins to increases, so Earth is moving further and further away. Velocity decreases because the gravitational force is weaker. This implies that the total energy is not conserved. Our results are consistent with those of the SHO. I think the Euler-Cromer method is best fit for this situation rather than the Euler method because of how inaccurate the approximation is.

![download-12](https://github.com/kobestenson/COMPPHYS/assets/156839835/fbf4859a-852d-4641-9ba7-4857f25e3e2a)


## Adapted Model

Below is the model of Mars. We can see that the same assumptions from Kepler's Laws apply to other planets within our solar system as well.

![download-11](https://github.com/kobestenson/COMPPHYS/assets/156839835/ff30f168-a89a-49bf-a4f7-17bf18eda2bf)



