---
category: [Neuroscience, Physics]
---

For periodic signals the frequency is simply defined as the number of repeats per unit time or 1 over the period duration:  
$$ f = \frac{1}{T} $$  
But what if the frequency changes over time? Take as an example the ZAP stimulus shown in figure 1 that is used in neuronscience to investigate resonance properties of neurons. The ZAP stimulus is defined as a sinusoid that has a frequency which increases linear with time.  

![png]({{ site.url }}{{ site.baseurl }}/images/Instantaneous-Frequency/ZAP_stimulus.png)
Figure 1: The ZAP stimulus.  

To derive the formula for the ZAP stimulus we need a definition of frequency as a function of time - the instantaneous frequency. The instantaneous frequency is defined as the derivative of the phase (point at which you are in your period usually defined in radians) divided by the total period (correspondingly $$ 2 \pi $$).  
$$ f(t) = \frac{\delta \phi}{\delta t} \cdot \frac{1}{2 \pi} $$  
So instead of the coarse grained definition of 1 period per period duration we now have part of the period per infinitely small time bin.

Now lets try to use this definition to derive the formula for the ZAP stimulus.  
Formular for the linear increasing frequency:  
$$ \begin{equation}
f(t) = f_0 + \frac{f_1 - f_0}{T} \cdot t \tag{1}
\end{equation} $$
Formular for the phase which will be used as argument for the sine (rearranging the definition of the instantaneous frequency): 
$$ \begin{equation}
\frac{\delta \phi}{\delta t} = 2 \pi \cdot f(t) \tag{2}
\end{equation} $$  
Insert (1) in (2):  
$$ \begin{equation}
\frac{\delta \phi}{\delta t} = 2 \pi \cdot f_0 + \frac{f_1 - f_0}{T} \cdot t \tag{3}
\end{equation} $$  
Integrate:  
$$ \begin{align}
\phi(t) &= 2 \pi \int^t_0 f_0 + \frac{f_1 - f_0}{T} \cdot \tau \delta\tau
&= 2 \pi [f_0 \tau + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot \tau^2]^t_0 $$  
&= 2 \pi (f_0 \cdot t + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot t^2) \tag{4}
\end{align} $$  
Thus, the formula for the ZAP stimulus is:  
$$ \begin{equation}
ZAP(t) = \sin(2 \pi (f_0 \cdot t + \frac{1}{2} \frac{f_1 - f_0}{T} \cdot t^2)) \tag{5}
\end{equation} $$  
