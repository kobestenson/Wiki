# Goals

The goal of the lab was to implement and model the Fourier Transform. The Fourier Transform allows us to take the the sum of sine and cosine functions and go from a function of time to a function of frequency. We look in multiple situations like sunspots and instrument tunes. We also implement the inverse Fourier Transform as well.

# Part 1

To start out the lab, we take the general form of the cosine function, $f(t) = Acos(\omega t + \phi)$, and then graphed the sum of each individual curve. We did this to see a visual representation of the function we would be using within the Fourier Transform. Below is the three cosine functions and the sum of the functions.

![download-7](https://github.com/kobestenson/COMPPHYS/assets/156839835/5533e9b5-2308-4d2c-9b02-4c52a0bc0669)

Next, we import the numpy fft module to compute the Fourier Transform of our summed wave. The goal of the numpy module is to convert the signal into something we can easily read.

```python
n=len(t)

power = np.abs(Y[1:int(n/2)])/(n/2+1)# the power

# the following code converts the time array to a frequency array
TMAX = (t[1]-t[0])*(n-1)
df = 1/TMAX # this is the lowest frequency we can sample
frequency=np.arange(int(n/2))*df
```

This code allows use the frequency integral from the slides and created the graph of Power versus Frequency:

![download-9](https://github.com/kobestenson/COMPPHYS/assets/156839835/5b58e14f-f1f5-41b7-9b92-431e6cd43775)

