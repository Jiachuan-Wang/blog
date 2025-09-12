---
title: 'Study Notes on Neuronal Dynamics'
date: 2025-09-12
categories: [Notes, Neuroscience]
description: My study note for Neuronal Dynamics
tags: [Neuroscience]
pin: false
math: true
---

This is a study note for *Neuronal Dynamics* (Gerstner *et al.*).



# The passive membrane



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


# I&F Model



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



