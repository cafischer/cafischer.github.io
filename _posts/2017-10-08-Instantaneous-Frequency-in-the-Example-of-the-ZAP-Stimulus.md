---
category: Physics
---

For periodic signals the frequency is simply defined as the number of repeats per unit time or 1 over the period duration:  
$$ f = \frac{1}{T} $$
But what if the frequency changes over time? Take as an example the ZAP stimulus shown in figure 1 that is used in neuronscience to investigate resonance properties of neurons. The ZAP stimulus is defined as a sinusoid that has a frequency which increases linearly in time.   

![png]({{ site.url }}{{ site.baseurl }}/images/Instantaneous-Frequency/ZAP_stimulus.png)
Figure 1: The ZAP stimulus.   

To derive the formula for the ZAP stimulus we need a definition of frequency as a function of time which is called instantaneous frequency. It can be defined as the derivative of the phase (point at which you are in your period) divided by total period (usually 2 \cdot \pi).  
$$ f(t) = \frac{\delta \phi}{\delta t} \cdot \frac{1}{\pi} $$
So instead of 1 repeat per period we are now more precise and look at how far in the period did we get for a small time bin.  

Now lets try to derive the formula for the ZAP stimulus:  
linear increasing frequency:  
$$ f(t) = f_0 + \frac{f_1 - f_0}{T} \cdot t $$
we want to know the phase to use it as input argument for the sign, rearranging the definition of the instantaneous frequency gives:  
$$ \frac{\delta \phi}{\delta t} = 2 \pi \cdot f(t) $$
insert (1) in (2):  
$$ \frac{\delta \phi}{\delta t} = 2 \pi \cdot f_0 + \frac{f_1 - f_0}{T} \cdot t $$
integrate: 
$$ \phi(t) = 2 \pi \integral^t_0 f_0 + \frac{f_1 - f_0}{T} \cdot \tau \delta\tau = 2 \pi [f_0 \tau + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot \tau^2]^t_0 = 2 \pi (f_0 \cdot t + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot t^2) $$
Thus the formula for the ZAP stimulus is:  
$$ ZAP(t) = sin(2 \pi (f_0 \cdot t + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot t^2)) $$
