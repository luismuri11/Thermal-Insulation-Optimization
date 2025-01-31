# Case Studies: Thermal Insulation Optimization
In this example, we will use an Artificial Neural Network (ANN) to design thermal insulation around tubes in order to minimize heat loss. You will later implement this in Python.

A fluid flows through three tubes, each of diameter d and length L. Surrounding each tube is a layer of thermal insulation material with thicknesses $t_1$, $t_2$, $t_3$, and thermal conductivities $k_1$, $k_2$ and $k_3$, respectively. The thermal resistance of the insulation around each tube, $R_i$, is calculated as:
​

$R_i = \frac{t_i}{{\pi}{d}{L}{k_i}}$
 
The total heat loss through the insulation is: 

$Q_{all} = \frac{{\Delta}{T}}{R_1}+\frac{{\Delta}{T}}{R_1}+\frac{{\Delta}{T}}{R_1}$
​
 
In the equations above, $\Delta{T}$ represents the temperature difference between fluid and the environment. 

Thicker insulation is preferred as it reduces heat loss; however, the thickness is constrained by the total cost, P, which is given by

${c_1}{\pi}{d}{L}{t_1} + {c_2}{\pi}{d}{L}{t_2} + {c_3}{\pi}{d}{L}{t_3} = P$

where $c_i$ represents the cost per unit volume of each insulation material.

Normalizing the layer thickness by d and defining $x_i = \frac{t_i}{d}$, the goal is to minimize

$Q = \frac{Q_{all}}{{\Delta{T}}{\pi}{L}{k_1}} = \frac{1}{x_1} + \frac{k_2}{{k_1}{x_2}} + \frac{k_3}{{k_1}{x_3}}$

with the following constraint  

$x_1 + {\frac{c_2}{c_1}}{x_2} + {\frac{c_3}{c_1}}{x_3} = \frac{P}{{\pi}{d^2}{L}{c_1}}$

For a specific case, assume insulation material 1 has the best insulating properties, while the other materials are more conductive, with $\frac{k_1}{k_2}=1.5$ and $\frac{k_3}{k_1}=2.0$. The most insulative materials are more expensive, while the less insulative materials are less costly. Assuming $\frac{c_2}{c_1}=0.5$ and $\frac{c_3}{c_1}=0.2$, and $\frac{P}{{\pi}{d^2}{L}{c_1}}=0.3$, the optimization target becomes minimizing

$Q = \frac{1}{x_1}+\frac{1.5}{x_2}+\frac{2.0}{x_3}$
 
with the following constraint

$x_1 + {0.5}{x_2} + {0.2}{x_3} = 0.3$

We first develop an ANN model to serve as a surrogate for the objective function. This ANN model is then integrated with a gradient-based optimization algorithm to optimize the design variables $x_1$, $x_2$, $x_3$ and achieve the minimum value of 𝑄.
