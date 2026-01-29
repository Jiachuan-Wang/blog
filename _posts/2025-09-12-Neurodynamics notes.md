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



### **The passive membrane**



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



For a single pulse, suppose the duration is short: 


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

### **I&F model**



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



### **Synapses & dendrites**

#### Synapse

Synaptic current can be modeled by:


$$
-I^{syn}(t)=-g^{syn}(t)(u-E_{syn})
$$



And $$g(t)$$  can be modeled by exponential decay (and rise):


$$
g(t)=\sum_k \bar{g}_{syn} e^{-\frac{t-t_k}{\tau}} [1-e^{-\frac{t-t_k}{\tau_{rise}}}]\Theta(t-t_k)
$$


AMPAR and GABAAR have rapid temporal dynamics, while NMDAR and GABABR are slow.

$$E_{syn}$$ for excitatory synapse is ~0 mV, and ~75 mV for inhibitory synapses. The same spike would have small effect at the inhibitory synapses at resting potential. If it’s at exactly reversal potential, the driving force will be 0 (shunting inhibition).



#### STP

In Dayan-Abbott model (2001), the amount of "ready-to-use" neurotransmitter is represented by $$P_{rel}$$.

And the maximum synaptic conductance $$\bar{g}_{syn}=c P_{rel}$$.



For depression:


$$
\frac{d P_{rel}}{dt}=-\frac{P_{rel}-P_0}{\tau_P}-f_D P_{rel} \sum_k \delta (t-t_k)
$$


For facilitation:


$$
\frac{d P_{rel}}{dt}=-\frac{P_{rel}-P_0}{\tau_P}-f_F (1-P_{rel}) \sum_k \delta (t-t_k)
$$


On the right side, the first term indicates that $$P_{rel}$$ would be back to the steady state $$P_0$$ exponentially (with a time constant $$\tau_P$$).



#### Cable equation

First, the current at time $$t$$, location $$x$$ can be written as:


$$
I(t,x)=c \frac{du(t,x)}{dt}+\sum_{ion} I_{ion}(t,x)
$$


Two locations between the resistor are $$x$$ and $$x+dx$$, and the $$R_L$$ is the longitudinal resistance.

So, $$I$$ can also be described as external current injection plus current arriving and leaving:


$$
I(t,x)=I^{ext}(t,x)+I_L(t,x)-L(t,x+dx)= I^{ext}(t,x)+\frac{u(t,x-dx)-2u(t,x)+u(t,x+dx)}{R_L}
$$


If we downscale the $dx$:


$$
R_L=r_L dx, C=c dx, I_{ion}=i_{ion} dx, I^{ext}=i^{ext} dx
$$


We get the cable equation (by combining the two expressions regarding $$I(t,x)$$):


$$
\frac{d^2u(t,x)}{d^2x}=c r_L \frac{d u(t,x)}{dt} + r_L \sum_{ion} i_{ion} (t,x) - r_L i^{ext}(t,x)
$$





### **Two-dimensional models and phase plane analysis**

#### Reduce the 4D HH model to 2D

Assumption: dendrites are approximated as passive (leak only), which leads to a point neuron.

Tricks:

- Separation of time scales. Dynamics of m is fast, so $$m(t)=m_0(u(t)))$$

Why? For coupled differential equations


$$
\begin{cases} 

   \tau_1\frac{dx}{dt}=-x+h(y) \\

   \tau_2\frac{dy}{dt}=f(y)+g(x)

  \end{cases}
$$


If $$\tau_1\ll\tau_2$$, x will approach the value of h(y) exponentially, so $$x=h(y)$$

Then $$\tau_2\frac{dy}{dt}=f(y)+g(h(y))$$

Also note that “dynamics of m is fast” means comparing with the dynamics of n, h, and I(t).

- Dynamics of h and n are similar, so $$1-h(t)=an(t)=w(t)$$

Now HH model is reduced to 

$$
c\frac{du}{dt}=-g_{Na}m^3_0(u)(1-w)(u-E_{Na})-g_K[\frac{w}{a}]^4(u-E_K)-g_l(n-E_l)+I(t)
$$

 

$$
\frac{dw}{dt}=-\frac{w-w_0(u)}{\tau_{eff}(u)}
$$

 

So it’s a 2D system:

 

$$
\begin{cases} 

   c\frac{du}{dt}=f(u(t),w(t))+I(t) \\

   \frac{dw}{dt}=g(u(t),w(t))

  \end{cases}
$$



The notes regarding phase plane analysis are omitted, as I don't want to plot the figures.



#### Further reduction to 1D

For $$\tau_u \ll\tau_w$$, the flux is nearly horizontal on the w-u phase plane.

 

So $$\tau_w \frac{dw}{dt}\approx 0$$, which means $$w\approx w_{rest}$$ when not spiking.

 

Then $$\tau \frac{du}{dt}=F(u,w_{rest})+RI(t)=F(u)+RI(t)$$, which is the nonlinear I&F model (see previous notes).



### **Variability of spike trains**

#### Source of variability

1. Intrinsic noise from ion channels.
2. Network noise from other neurons.

*In vitro* single-neuron recordings using **fluctuating current stimulation showed reliable spike timing** (Mainen and Sejnowski, 1995), indicating that the variability largely arises from network noise.

The variability can be described by the distribution of interspike interval (ISI), which accounts for the regularity.



#### Definitions of firing rate/rate codes

1. Temporal average: $$v(t)=\frac{n^{sp}}{T}$$. Examine the distribution of ISI (regularity of spike train), or the Fano factor (repeatability across trials).
2. Average across repetitions: count the spike numbers in a very short time window. Examine the **peristimulus time histogram** $$PSTH(t)=\frac{n(t;t+\Delta t)}{K\Delta t}$$.
3. Population averaging: population activity $$A(t)=\frac{n(t;t+\Delta t)}{N\Delta t}$$.

Seems the population activity is the one used by animals.



#### Homogeneous Poisson model

Assumes neuron fires at a **constant rate** $$\rho_0$$ during time $$T$$.

Probability of finding a spike in $$\Delta t$$: $P_F = \rho_0 \Delta t$.

Survivor function, describing ISI: $$S(t)=e^{-\rho_0 t}; S(0)=1$$. This is in continuous time steps. In discrete time steps:  $$S(t)=(1-\rho_0 \Delta t)^{\frac{t}{\Delta t}}$$.



#### Inhomogeneous Poisson model

Probability of firing: $P_F = \rho(t) \Delta t$.

Survivor function (estimate the probability of survival at time $$t$$ given a spike at time $$\hat{t}$$): 
$$
S(t\vert\hat{t})=e^{-\int_{\hat{t}}^t \rho(t^\prime) dt^\prime}
$$
.

Interval distribution: $$P(t\vert\hat{t})=\rho(t) S(t\vert \hat{t})$$.



#### Stochastic spike arrival

The total spike train of $$K$$ presynaptic neurons $$S(t)=\sum_{k=1}^{K} \sum_f \delta (t-t_k^f)$$.

The expectation at each moment of time is the rate $$\langle S(t) \rangle = K \rho_0$$.



The synaptic current $$I(t)$$ sums up $$K$$ neurons and firing time f. 

$$\mu = \langle I(t) \rangle=\langle \frac{1}{R}\sum_k w_k  \sum_f \alpha (t-t_k^f)\rangle=\frac{1}{R} \sum_k w_k \int \alpha(s) \langle   \sum_f  \delta (t-t_k^f-s) ds\rangle = \frac{1}{R} \sum_k w_k \int \alpha(s) ds \rho_0 $$



##### Fluctuation of potential 

As $$\langle x(t) \rangle=\int f(s) ds \rho_0$$,

Autocorrelation $$\langle x(t) \hat{x}(t)\rangle = \int dt^\prime \int dt^{\prime\prime} f(t-t^\prime) f(t-t^{\prime\prime}) \langle S(t^\prime)S(t^{\prime\prime})\rangle$$



Probability of spike in step $$n$$ and $$k$$:

For $$n \neq k$$, $$P(n,k)=P_F P_F = \rho_0^2 (\Delta t)^2$$; For $$n=k$$, $$P(n,n)=P_F=\rho_0 \Delta t$$.

Taking $$\Delta t \rightarrow 0$$, autocorrelation in continuous time steps is $$\langle S(t)S(t^{\prime})\rangle=\rho_0 \delta(t-t^\prime)+\rho_0^2$$. (by dividing $$\Delta t$$ in the discrete autocorrelation. The diagonal contribution ($$n=k$$) becomes infinitely sharp and turns into a Dirac delta.)



### **Noise models**

1. Diffusive noise.
2. Escape noise (can estimate time-dependent interval distribution)

Escape rate (stochastic intensity of point process) $$\rho(t)=f(u(t)-\theta)$$

$$f(u-\theta)$$ can be $$\frac{1}{\Delta}e^{\frac{u-\theta}{\Delta}}$$ or $$ReLU(\rho_0[\frac{u}{\theta}-1])$$.

<br>

Survivor function (probability to survive w/o firing again up to time $$t$$) has $$\frac{d}{dt}S_I(t\vert \hat{t})=-\rho(t)S_I(t\vert \hat{t})$$, where $$\hat{t}$$ is the last firing time.

So $$S_I(t\vert \hat{t})=e^{-\int_\hat{t}^t \rho(t^\prime)dt^\prime}$$.

And the ISI $$P(t\vert \hat{t})=\rho(t)S(t\vert \hat{t})$$.

<br>

In discrete time, the probability to survive 1 time step $$S(t_{k+1} \vert t_{k})=e^{-\rho(t_k)\Delta}$$,

and the probability to fire in 1 time step $$P_k^F=1-S(t_{k+1} \vert t_{k})$$.

<br>

The Likelihood of a spike train $$L(t^1,...,t^N)=e^{-\int_0^T \rho(t^\prime) dt^\prime}\prod_{f=1}^N \rho(t^f)$$

Can be transformed into log-likelihood.



#### Rate codes vs. temporal codes

* Rate codes
  * Population rate
* Temporal codes
  * Time to first spike (after input)
  * phase (wrt oscillation) of spike 
  * stochastic resonance





### **Modern phenomenological neuron models**

#### Add adaptation to EIF

$$\tau \frac{du}{dt}=-(u-u_{rest})+\Delta e^{\frac{u-\vartheta}{\Delta}}-R\sum_k w_k +RI(t)$$

where the dynamics of $$w_k$$ is $$\tau_k \frac{dw_k}{dt}=a_k(u-u_{rest})-w_k+b_k\tau_k\sum_f \delta(t-t^f)$$.

The $$a_k$$ is the coupling parameter. The last term means after each spike, $$w_k$$ jumps by an amount $$b_k$$.

So after a spike, we do this jump and reset.



#### Add dynamical threshold to EIF

The threshold increases after each spike:

$$\vartheta =\theta_0+\sum_f \theta_1(t-t^f)$$



#### Adaptive LIF & SRM

The two linear equations ($$u$$ and $$w$$ dynamics) can be integrated:


$$
u(t)=\sum_f \eta (t-t^f)+\int_0^{\infty}ds\kappa(s)I(t-s)+u_{rest}
$$


and still there are dynamical threshold and reset event.



The terms in the equation above can be rewritten as


$$
\int \eta(s) \sum_f \delta(t-t^f-s)ds = \int_0^\infty \eta(s)S(t-s)ds
$$
where $$S(t)$$ is the spike train.

Linear filters are applied for input, threshold, and refractoriness.



### **Neuronal populations**

One population means neurons in one layer of one column.

#### Mean-field argument

Assume a **fully connected** homogeneous network (all neurons and synapses are the same; each neuron receives the same external input).


$$
I_i^{syn}(t)=\sum_f \sum_k w_{ik}\alpha(t-t_k^f)=\sum_f \sum_k w_{ik}\int\alpha(s)\delta(t-t_k^f-s)ds=w_0\int \alpha(s)A(t-s)ds
$$


where $$w_{ik}=\frac{w_0}{N}$$.



Interpretation: all neurons receive the same total input current.



#### Stationary mean-field and asynchronous state

At the stationary state, for a fully connected homogeneous network with constant input:

1. Input is constant and identical for all neurons.
   $$
   I_0=w_0 \int \alpha(s)dsA_0+I_0^{ext}
   $$

2. Frequency (single-neuron gain function):
   $$
   v=g(I_0)
   $$

3. Single neuron rate = population rate:
   $$
   v=A_0
   $$



In a stationary state of asynchronous firing, solutions might be found in the $$I_0 - A_0$$ plane by combining the three equations.



#### Random networks

In a homogeneous network with random connectivity (with a connection probability $$p$$ or fixed number of inputs $$K$$), the equations above hold.



