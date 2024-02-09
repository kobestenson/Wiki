# Background

## Ordinary Differential Equation
An ordinary differential equation (ODE) is an equation that relates a function with one variable to its derivatives with respect to the variable that is present up to a certain order within the equation. This equation describes how the function will change over time.

## Taylor Expansion
The Taylor expansion is an approximation of a function near a given point by an infinite sum of terms of its derivatives. The general form is, where f(x) is the function and "a" is the point:
$f(x) = f(a) + f'(a)(x-a) + \frac{f"(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 ...$

## Euler Method
The Euler method is used to approximate solutions to the ODEs numerically. We find our solution by taking the derivatives and approximating for the function. The first order of the Euler method is $\frac{dy}{dx} = f(x_n,y_n)$ with an initial condition of $y(x_0) = y_0$. Our general form for the Euler method is $y(n+1) = y_n + h*f(x_n,y_n)$ where $y_n$ is the approximation of $x_n$, $h$ is the time step, and $f(x_n,y_n)$ is the derivative of $y$ with respect to $x$.

# In The Lab & Lecture
## Lab
### Euler Method
In the lab, we use the Euler method to calculate the number of radioactive nuclei that survive as a function of time. For our example, we used Uranium 235, but this could apply to any radioactive nuclei and/or radioactive decay. The differential equation we use to represent the decay is: 

$\frac{dN}{dt} = \frac{-N}{T}$ where T represents tau.

We are able to use this function in our Taylor Expansion because our function is equal to: $N(t + \triangle t) = N(t) + \frac{dN}{dt}(\triangle t)$

The Euler method in our case represents Uranium's half-life as the Taylor Expansion updates over the course of a set time.

### Analytical Solution
With our equation to represent decay, we use the steps we learned through the differential equations course to find our analytical solutions. The steps we take to find our solution is separation of variables, integration, and raising each side to its exponential. This gives us the analytical solution of: 

$N(t) = N_0 * e^-\frac{1}{T}$

Our analytical solution is important because it allows us to have a reference while making a comparison to our approximation made during the Euler method. This allows us to check our accuracy and precision. Connecting back to the lab, our approximation and analytical solution were shown side-by-side to show the accuracy of our Euler method

<img width="1000" alt="Screen Shot 2024-02-08 at 7 36 15 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/42d2d62b-3266-4d2f-ba09-cc0c840f5598">

### Effect of Time Step
Time step is very important to find making approximations during the use of the Euler method. While testing multiple time steps within the lab, it is evident that higher time steps create less accurate solutions. Below is a graph of our analytical solution along with time steps of  0.05, 0.2, and 0.5 seconds.

<img width="998" alt="Screen Shot 2024-02-08 at 7 41 48 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/6444b0c7-ca09-449c-9dd3-47c9b98ee17f">

As you can see, the as time steps become closer to 0, more data points are created, meaning the graph has a smoother line and set of data. This correlates to greater accuracy as well because the data is more similar to the analytical solutions graph. 

## Lecture
In the lecture, we reinforced our understanding of the Euler method and why it may be so useful. We are able to take real world situations and approximate specific solutions that correspond to this problem. In our case, we approximated a bicyclists velocity over a certain period of time while also using the bicyclists power output. This is important because the Euler method is being used to compute complex problems. This allows the Euler method to become universal by factoring outside forces like air resistance. Below is my graph of using the Euler method while factoring no air resistance and air resistance:

<img width="524" alt="Screen Shot 2024-02-08 at 8 02 24 PM" src="https://github.com/kobestenson/COMPPHYS/assets/156839835/854144cf-6861-480a-848b-f04624c8cb2a">

Just like in the Lab, time step determines how accurate the results of the Euler method will be. One issue someone may face when determining a time step might be not knowing what size to use. In both the Lecture and Lab, we were given values to use for the time step, but if I weren't given a value for the time step, I would use trial and error and compare to my analytical solution or I would look at how accurate I would need to be for the problem given. 