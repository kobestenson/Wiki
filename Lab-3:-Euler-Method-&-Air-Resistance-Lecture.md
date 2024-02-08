# Background

## Ordinary Differential Equation
An ordinary differential equation (ODE) is an equation that relates a function with one variable to its derivatives with respect to the variable that is present up to a certain order within the equation. This equation describes how the function will change over time.

## Taylor Expansion
The Taylor expansion is an approximation of a function near a given point by an infinite sum of terms of its derivatives. The general form is, where f(x) is the function and "a" is the point:
$f(x) = f(a) + f'(a)(x-a) + \frac{f"(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 ...$

## Euler Method
The Euler method is used to approximate solutions to the ODEs numerically. We find our solution by taking the derivatives and approximating for the function. The first order of the Euler method is $\frac{dy}{dx} = f(x_n,y_n)$ with an initial condition of $y(x_0) = y_0$. Our general form for the Euler method is $y_(n+1) = y_n + h*f(x_n,y_n)$ where $y_n$ is the approximation of $x_n$, $h$ is the time step, and $f(x_n,y_n)$ is the derivative of $y$ with respect to $x$.

# In The Lab & Lecture

## Euler Method

## Analytical Solution

## Effect of Time Step

