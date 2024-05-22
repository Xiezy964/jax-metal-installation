# Ginzburg-Landau Equation

The governing equations for the microstructure evolution are the timedependent Ginzburg-Landau equation (also known as Allen-Cahn equation):[2021, Yang et. al]
$$
\begin{align}
\frac{\partial \eta_{i}(\mathbf{r}, t)}{\partial t} = -L_{\mathrm{g}} \frac{\delta F\left(\zeta, \eta_{i}, T\right)}{\delta \eta_{i}(\mathbf{r}, t)}
\end{align}
$$

Notice that to solve the right hand of this equation, the variation of functional $F$ (total free energy) with respect to the function $\eta_{i}$ (grain orientation) needs to be calculated. 

The functional F is given as: 
$$
\begin{align}
F(\eta_i,\nabla \eta_i) &= \int_V (f_{\text{local}} + f_{\text{grad}})dV \\
&=\left[ \sum_{i=1}^{n} \left( \frac{(\eta_i)^4}{4} - \frac{(\eta_i)^2}{2} \right) + \gamma \sum_{i=1}^{n} \sum_{\substack{j=1 \\ j \neq i}}^{n} (\eta_i)^2 (\eta_j)^2 + \frac{1}{4} + (1 - \zeta)^2 \sum_{i=1}^{n} (\eta_i)^2 + \frac{\kappa_p}{2} (\nabla \zeta)^2 + \frac{\kappa_g}{2} (\nabla \eta_i)^2\right]       \nonumber
\end{align}
$$

Considering a functional $\mathcal{F}$ which maps a function $u$, the variation is defined as:
$$
\begin{align}
\delta \mathcal{F}[u; \phi ]&=\lim _{\tau \to 0}{\frac {\mathcal{F}[u +\tau \phi ]-\mathcal{F}[u ]}{\tau }} \nonumber \\
&=\left[{\frac {d}{d\tau }}\mathcal{F}[u +\tau \phi ]\right]_{\tau =0}
\end{align}
$$

When handling with the variation of functional $F$ with respect to the function $\eta_{i}$, there is a similar form as the definition above:
$$
\begin{align}
\delta F[\eta_i; q ]&=\lim _{\epsilon \to 0}{\frac {F[\eta_i +\epsilon q ]-F[\eta_i]}{\epsilon }} \nonumber \\
&=\left[{\frac {d}{d\tau }}F[\eta_i +\epsilon q ]\right]_{\epsilon =0}
\end{align}
$$

We can use the definition to change the variation process to a derivative process. To fully understand the process, we may need to refer to some videos (see [bilibili](https://www.bilibili.com/video/BV1A7411N7mD/?spm_id_from=333.337.search-card.all.click)), and integration by part and divergence theorem will be utilized in this case. 

But if you konw the variation expression already, which is:
$$
\delta F(x,y,z)=\frac {\partial F}{\partial x}\delta x + \frac {\partial F}{\partial y}\delta y + \frac {\partial F}{\partial z}\delta z
$$

Then we can write the variation of $F$ as:
$$
\begin{align}
\delta F(\eta_i,\nabla \eta_i) &= \int_V (\frac {\partial f}{\partial \eta_i}\delta \eta_i + \frac {\partial f}{\partial \nabla \eta_i}\delta \nabla \eta_i)dV \\
&= \int_V [(\frac {\partial f}{\partial \eta_i} + \nabla \cdot \frac {\partial f}{\partial \nabla \eta_i})\delta \eta_i]dV \notag
\end{align}
$$

Now we can known the Euler-Lagrange expression of this equation and get:
$$
\begin{align}
\frac{\delta F\left(\zeta, \eta_{i}, T\right)}{\delta \eta_{i}(\mathbf{r}, t)}=\frac {\partial f}{\partial \eta_i} + \nabla \cdot \frac {\partial f}{\partial \nabla \eta_i}
\end{align}
$$

Now, to solve equation 6, we can separately solve it in the time and space domain. In the time domain, explicit Euler method:
$$
\begin{align}
\frac{\partial \eta_{i}(\mathbf{r}, t)}{\partial t}=\frac{\eta_i^{t+1}-\eta_i^{t}}{\Delta t}=-L_{\mathrm{g}} \frac{\delta F\left(\zeta, \eta_{i}, T\right)}{\delta \eta_{i}(\mathbf{r}, t)} \\
\eta_i^{t+1}=\eta_i^{t}-\Delta t \cdot -L_{\mathrm{g}} \frac{\delta F\left(\zeta, \eta_{i}, T\right)}{\delta \eta_{i}(\mathbf{r}, t)}
\end{align}
$$

In time domain, we use second-order central finite difference method:
$$
f''(x) \approx \frac{\delta_h^2 [f](x)}{h^2} = \frac{\frac{f(x+h) - f(x)}{h} - \frac{f(x) - f(x-h)}{h}}{h} = \frac{f(x+h) - 2f(x) + f(x-h)}{h^2}\\
\nabla^2 \eta_i=\frac{\partial^2 \eta_i}{\partial x^2} + \frac{\partial^2 \eta_i}{\partial y^2} + \frac{\partial^2 \eta_i}{\partial z^2} =\\
\frac{\Delta \eta_{ix^+}-2\eta_i+\Delta \eta_{ix^-}}{h^2} + \frac{\Delta \eta_{iy^+}-2\eta_i+\Delta \eta_{iy^-}}{h^2} + \frac{\Delta \eta_{iz^+}-2\eta_i+\Delta \eta_{iz^-}}{h^2}
$$

