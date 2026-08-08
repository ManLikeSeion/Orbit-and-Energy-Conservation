# Orbit-and-Energy-Conservation
A numerical simulation of Earth's orbit around the Sun using Python. It implements the Verlet integration method to calculate position, velocity, and energy states over three years, demonstrating total energy conservation in symplectic integrators compared to standard ODE solvers.

# Earth-Orbit-Verlet-Simulation

### Project Overview
In this project, I modelled the orbital dynamics of the Earth around the Sun to observe the system's kinetic, potential, and total mechanical energy over time. I chose to implement the Verlet integration method from scratch using Python and `numpy` rather than relying on standard ODE solvers. This choice was deliberate; symplectic integrators like the Verlet method are specifically designed to preserve the physical properties of Hamiltonian systems, ensuring that total energy remains strictly conserved over long periods. 

---

### 1. Mathematical Foundation
The core of the simulation relies on Newton's law of universal gravitation. The equations of motion for the position $(x(t), y(t))$ of the Earth in its orbital plane are defined by the following second-order differential equations:

$$\frac{d^{2}x(t)}{dt^{2}}=-G\,M\,\frac{x(t)}{r^{3}}$$

$$\frac{d^{2}y(t)}{dt^{2}}=-G\,M\,\frac{y(t)}{r^{3}}$$

where $r=\sqrt{x^{2}+y^{2}}$ represents the distance between the Earth and the Sun.

---

### 2. Physical Constants and Initial Conditions
To ensure physical accuracy, I worked entirely in SI units. I defined a unified parameter tuple, `par`, structured precisely in the order (G, M, m) to pass cleanly into my functions:

*   **Gravitational Constant (G):** $6.6738 \times 10^{-11} \text{ m}^3\text{kg}^{-1}\text{s}^{-2}$
*   **Mass of the Sun (M):** $1.9891 \times 10^{30} \text{ kg}$
*   **Mass of the Earth (m):** $5.9722 \times 10^{24} \text{ kg}$

For the starting state of the simulation, I set the initial position vector to $\mathbf{r}_0 = (1.521 \times 10^{11}, 0) \text{ m}$ and the initial velocity vector to $\mathbf{v}_0 = (0, 2.9291 \times 10^4) \text{ m/s}$. 

---

### 3. Implementation Details
I built the project in a modular way using Python, relying on `numpy` for vector calculations and `matplotlib` for data visualisation. I broke down the physics and numerical integration into dedicated functions:

*   **`get_acc(r, par)`**: Calculates the gravitational acceleration at a given position vector.
*   **The Integration Engine (`solve(par, r_s, v_s)`):** Implements the Verlet method to solve the equations of motion. I set the time-step resolution to one hour ($\Delta t = 3600 \text{ s}$) and ran the simulation for a total period of three years. This function returns the position array $r(t)$ and velocity array $v(t)$ as a tuple.
*   **Potential Energy Calculation (`potentialEnergy(r, par)`):** Computes the gravitational potential energy at any given position $r(t)$. Since this is a bound orbital system, these values are appropriately negative.
*   **Kinetic Energy Calculation (`kineticEnergy(v, par)`):** Computes the kinetic energy of the Earth based on the velocity array $v(t)$.

---

### 4. Data Visualisation and Analysis
Once the orbital data was generated, I analysed the energy of the system by creating two distinct visualisations. Because I used SI units, the resulting energy values were massive—on the order of $10^{33} \text{ J}$. 

1.  **Superimposed Energy Plot (`energy.png`):** I plotted the kinetic energy, potential energy, and total energy on a single canvas. This clearly visualised how the kinetic and potential energies continuously exchange and perfectly mirror each other as the Earth moves through its elliptical orbit, while the total energy line remains visibly flat.
  <img width="1000" height="400" alt="energy" src="https://github.com/user-attachments/assets/bd62caa7-c182-4466-89cb-01a91665a8e3" />

3.  **Total Energy Conservation Plot (`totalcons.png`):** To truly test the Verlet method, I created a second plot showing *only* the total energy as a function of time, zoomed in closely. This revealed the microscopic oscillating character characteristic of the Verlet algorithm, while proving that the mean total energy remained constant to an exceptionally high precision over the full three-year period.
<img width="1000" height="600" alt="totalcons" src="https://github.com/user-attachments/assets/d1993d58-f097-446d-903e-50a4e13fbe52" />
