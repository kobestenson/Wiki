# Goals

The goals of this lab were to incorporate the Fourier transform that we learned in a previous lab and lecture to help analyze seismic data taken in Mexico City during the 1985 earthquake. We are able to understand how environment factors can affect buildings and their safety factors. In this case, the condition of the soil added to the magnitude of the earthquake. We are also able to compare dominant frequencies in the surface waves with the natural frequencies of buildings.

# Overview

At the beginning of this lab, we used the ```!wget``` feature once again to load in all of the earthquake data. We were able to print a table with all of the features and measurements that were recorded. Below is a plot of latitude versus longitude:

![download-10](https://github.com/kobestenson/COMPPHYS/assets/156839835/1ff0ba69-b224-4a05-830f-18974c0a8994)

This graph is important because it shows us all of the earthquakes that have been recorded and gives a representation of the magnitude of each on by have larger or smaller points. We can conclude that most earthquakes do not happen in random areas. Most earthquakes happen within the same radius and/or follow trends. There are some random earthquakes here and there. These earthquakes are not evenly distributed across the surface because of the plate boundaries.

![download-11](https://github.com/kobestenson/COMPPHYS/assets/156839835/3d771b93-dc72-45be-a443-b4cf73946a8c)

From the data provided, we also realize that Mexico City's magnitude 8 earthquake is not very common. From the histogram above, a magnitude of 2.5-6 is the most common earthquake magnitude.

### Analyzing Seismic Waves

In this section, the goal was to read in data from the seismograph during the Mexico City earthquake, and show the illustrations created from time, acceleration, velocity, displacement.

![download-12](https://github.com/kobestenson/COMPPHYS/assets/156839835/baffbe86-7ec3-4668-9109-6ee7352373fe)

With the time series data above, we can see oscillations happening for about 6-8 seconds around the 56-64 second mark on the plot. This is important because we are able to read how intense the seismic waves truly were over the course of time. Without the limit on the time axis, we are able to understand that the waves do not have much of an impact until this range was closely focused on.

Given the data from the time series, we are able to create frequency spectrums that show the amplitudes of each frequency. This section was very in-depth due to the Fourier transform code.

```python
from numpy.fft import fft

Faccel = np.fft.rfft(mexico_equakes['accel'])
Fvel = np.fft.rfft(mexico_equakes['vel'])
Fdispl = np.fft.rfft(mexico_equakes['displ'])

n=len(mexico_equakes['time'])

# the following code converts the time array to a frequency array
TMAX = (mexico_equakes['time'][1]-mexico_equakes['time'][0])*(n-1)
df = 1/TMAX # this is the lowest frequency we can sample
freq=np.arange(int(n/2))*df

nyquist = np.abs(freq[0:n//2+1])
nyquist_acc = np.abs(Faccel[0:n//2+1])
nyquist_vel = np.abs(Fvel[0:n//2+1])
nyquist_displ = np.abs(Fdispl[0:n//2+1])
```

In our code above, you can see that after taking our Fourier transform we used ```[0:n//2+1]``` to represent the Nyquist frequency. In the review section of the lab, it was explained that the Nyquist frequency is half of fmax. Below is a plot of the Nyquist frequency:

![download-14](https://github.com/kobestenson/COMPPHYS/assets/156839835/332baea7-0fed-4f1a-9795-2eead2d52b85)

![download-13](https://github.com/kobestenson/COMPPHYS/assets/156839835/1e70412a-9a8e-42e3-bd2b-4014851eb79a)

It is evident that at 0.5 Hz, the amplitude is at a maximum with many other significant amplitudes ranging from 0.35-0.55 Hz. We see that the frequencies have amplitudes that increase drastically from displacement, velocity, acceleration, but anything less than 0.35 or greater than 0.55 have consistent amplitudes for each function.

### Recommendations

From the lab, we learn that resonant frequency is represented by $f_0 = \frac{10}{N_s}$. Using this formula, we can understand that a 15 story building during the earthquake had a frequency of 0.67 Hz. This is important to understand because the resonant frequency is so close to the dominant frequency of 0.5 Hz. Because we apply the Nyquist transform, we understand the frequency is halved which would make tall builders even more dangerous during this earthquake. A building with 20 stories will resonate because its frequency of 0.5 has the greatest amplitude.

I would aim to build buildings that would have a resonant frequency greater than 0.6. This would force the construction of smaller buildings because it is a much safer decision due to amplitudes being much lower. Buildings with frequencies greater than 0.9 would be acceptable in this region incase another earthquake with a magnitude of 8 occured.

### Summary

It was important to analyze seismic data because it gives us a better idea on how to breakdown seismic waves. We were able to use the seismic data and implement the Fourier transform to help compare dominant frequencies to natural frequencies. This allows us to understand the Mexico City earthquake and how buildings are affected by certain frequencies and environmental conditions.