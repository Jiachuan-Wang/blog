---
title: 'Study Notes on Neuronal Dynamics'
date: 2025-09-12
categories: [Notes, Neuroscience]
description: ''
tags: [Neuroscience]
pin: false
math: true
---

This is a study note for *Neuronal Dynamics* (Gerstner *et al.*).



### The passive membrane



The **passive membrane** model can be described using an RC (resistor–capacitor) circuit, where


$$
I=I_R+I_C
$$


and


$$
I_C=\frac{dQ}{dt}=C\cdot\frac{du}{dt}
$$



$$
I_R=\frac{1}{R}(u-u_{rest})
$$


so


$$
R\cdot C\cdot \frac{du}{dt}=-(u-u_{rest})+R\cdot I(t); R\cdot C=\tau
$$


If we remove the battery:


$$
V=u-u_{rest}
$$

$$
\frac{dV}{dt}=\frac{d}{dt}(u-u_{rest})=\frac{du}{dt}
$$

$$
\tau \cdot \frac{dV}{dt}=-V+R\cdot I(t)
$$





The **pulse input** is modelled using Dirac's delta function:


$$
I(t)=q\cdot \delta(t-t_0)
$$


The total charge q is the area under the I vs. t curve.

Its effect on 
$$
u(t)
$$
 is to cause it jump from 
$$
u_{rest}
$$
 to a larger value (
$$
\frac{q}{C}
$$
) and then decay exponentially.



The properties of Dirac's delta function:


$$
\int_{t_0-a}^{t_0+a}\delta(t-t_0)dt=1
$$


and:


$$
\int_{t_0-a}^{t_0+a}f(t)\delta(t-t_0)dt=f(t_0)
$$



Next we want to solve for the membrane response 
$$
u(t)
$$
to the input current:



For a singe pulse, suppose the duration is short: 


$$
\Delta=t-t_0<<\tau
$$


The rise component is dominated by the first terms in the Taylor expansion of the exponential function, so:


$$
u(t)=u_{rest}+\frac{q}{C}e^{-\frac{t-t_0}{\tau}}
$$


For arbitrary inputs, the response is as follows:


$$
u(t)=u_{rest}+\int_{-\infty}^{t}\frac{1}{C}e^{-\frac{t-t^\prime}{\tau}}I(t^\prime) dt^\prime
$$


But this assumes that the input before 
$$
t_0
$$
has little contributions, otherwise


$$
u(t)=u_{rest}+[u(t_0)-u_{rest}]e^{-\frac{t-t_0}{\tau}}+\int_{t_0}^{t}\frac{1}{C}e^{-\frac{t-t^\prime}{\tau}}I(t^\prime) dt^\prime
$$

### I&F Model



The previous section discussed the subthreshold regime. To simulate firing, we basically need a passive membrane + threshold.



In LIF model, 


$$
\tau\cdot \frac{du}{dt}=-(u-u_{rest})+R\cdot I(t)
$$


If firing (
$$
u(t)=\vartheta
$$
), then


$$
u\rightarrow u_r
$$


In nonlinear I&F model, 


$$
\tau\cdot \frac{du}{dt}=F(u)+R\cdot I(t)
$$


The 
$$
F(u)
$$
can be quadratic or exponential. And the intrinsic threshold depends on the input. (Although we still have a reset condition.)



And we can draw an F (frequency)-I curve or gain function of the neuron. 



Seems that the EIF model fits the experimental data (layer-5 pyramidal cells; Badel *et al.*, *J Neurophysiol.*, 2008) best:


$$
F(u)=-(u-u_{rest})+\Delta_T e^{\frac{u-\vartheta}{\Delta_T}}
$$


We didn't consider the adaptation, noise, and other biophysical details yet.



### **Detailed ion-current based neuron models**

According to Boltzmann distribution


$$
c \propto e^{-\frac{E}{kT}}
$$


and because of


$$
E=q\cdot u
$$


we have the Nernst equation


$$
\Delta u = u_{in} - u_{out} = -\frac{kT}{q}ln\frac{c_{in}}{c_{out}}
$$


The 
$$
\Delta u
$$
describes a hypothetical equilibrium given the concentration difference across the cell membrane. This hypothetical equilibrium potential, or **reversal potential**, is specific to each ion. The total equilibrium potential is a compromise among the potentials of all ions.


$$
E_{Na}\approx+67 mV; E_K\approx-83 mV
$$


#### Hodgkin-Huxley model



The total current is the sum of capacity current, Na current, K current, and leak current (other channels):


$$
I(t)=I_c + I_{Na}+I_{K}+I_l
$$



Refer to the the previous notes...


$$
c \cdot\frac{du}{dt}=-I_{Na}-I_K-I_l+I(t)=-\frac{1}{R_{Na}}(u-E_{Na})-\frac{1}{R_{K}}(u-E_{K})-\frac{1}{R_{l}}(u-E_{l})+I(t)
$$


Considering the gating variables:


$$
c \cdot\frac{du}{dt}=-g_{Na}m^3h(u-E_{Na})-g_kn^4(u-E_{K})-g_l(u-E_{l})+I(t)
$$


For m, n, and h:


$$
\frac{dx}{dt}=-\frac{x-x_0(u)}{\tau(u)}
$$


#### Adaptation



Check [M current](https://en.wikipedia.org/wiki/M_current) and [persistent sodium current](https://en.wikipedia.org/wiki/Persistent_sodium_current).



