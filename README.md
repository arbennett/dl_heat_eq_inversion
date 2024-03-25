# Exploring numerical inverse modeling with deep learning from a "simplified" perspective

## Background
I started exploring this in response to some questions about feasibility of deep-learning based inverse modeling techniques for a much more complex topic. Disregarding all of that context, I'm aiming to understand some limitations and possibilities for using numerical forward modeling, deep-learning inverse modeling, and physically guided constraints.

## Problem statement: heat equation
The 1D heat equation is a partial differential equation that describes the distribution of heat in a system over time. The equation is given by:

$$
\frac{{\partial u(x, t)}}{{\partial t}} = \alpha(x) \frac{{\partial^2 u(x, t)}}{{\partial x^2}}

$$

where $u(x, t)$ represents the temperature at position $x$ and time $t$, $α$ is the thermal diffusivity. For the case of this experiment we generally consider a temporally constant diffusivity, though it may vary in space. The domain of the system will be fixed to $x\in[0,1]$.  To complete the problem description we require boundary conditions at $x=0$ and $x=1$.

For the sake of simplicity we will tie the boundary conditions and form of the diffusivity function together, making it easy to generate random instances. To generate the diffusivity functions we simply sample a number of Gaussian distributions with random mean and variance terms which will be used as the diffusivity. When sampling more than a single Gaussian, the overal result is averaged for each point in the domain. The boundary conditions are set by the min and max of the diffusivity, so that $u(x=0)=min(\alpha)$ and $u(x=1)=max(\alpha)$.

We solve the heat equation via the Crank-Nicholson implicit method, with a timestep of $dt=0.001$ and end time of $t_{end}=10.0$. One hundred gridpoints are used in the spatial discretization. 

## Experimental setup
### Basic setup for the "complete" inversion model
To set up the baseline model we 
