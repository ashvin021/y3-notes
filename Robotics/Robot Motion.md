- **Position and Motion of a Robot**
	- Coordinate Frames
		- Define 2 coordinate frames:
			1. World Frame ($W$)
			2. Robot Frame ($R$)
		- The world frame $W$ is anchored in the world, and the robot frame $R$ is carried by and stays fixed relative to the robot at all times.
		- The problem of finding where a robot is, is simply describing $R$ relative to $W$, i.e what is the transformation between the two frames.
	- Degrees of Freedom
		- rigid body that translates and rotates along 1D path - train - 1 DOF (1 translational)
		- rigid body that translates and rotates on 2D plane - ground robot - 3 DOF (2 translational, 1 rotational)
		- translates and rotates in 3D volume - flying robot - 6 DOF (3 translational, 3 rotational)
		- A **holonomic** robot is one that can move instantaneously in any direction in the space of its degrees of freedom.
		- Holonomic ground robot - possible with omnidirectional wheels

- **Standard Wheel Configurations**
	- The 2 configurations are both non-[[Holonomic|holonomic]] and both use 2 motors each.
	- Differential Drive
		- Two wheels, one on left and one on right side of the robot. Each driven by its own motor.
		- Steering is done by setting different wheel speeds.
			- Straight line motion if $v_L = v_R$
			- Turn on the spot if $v_L = -v_R$
		- Circular path of a differential drive robot
			- To find radius $R$ of curved path, consider a period of motion $\Delta t$ where a robot of width $W$ moves along a circular arc through angle $\Delta \theta$.
				- Left wheel: distance moved = $v_L \Delta t$; radius of arc = $R - \frac{W}{2}$
				- RIght wheel: distance moved = $v_R \Delta t$; radius of arc = $R + \frac{W}{2}$
				- Both wheel arcs subtend the same and  $\Delta \theta$ so:
					- $$\Delta \theta = \frac{v_L \Delta t}{R - \frac{W}{2} } = \frac{v_R \Delta t}{R + \frac{W}{2}}$$
					- $$ \frac{W}{2}(v_L + v_R) = R(v_L - v_R)$$
					- $$R = \frac{W(v_L + v_R)}{2(v_L - v_R)}$$
					- $$\Delta \theta = \frac{(v_R - v_L)\Delta t}{W}$$
					- [[Pasted image 20230315213006.png]]
	- Drive and steer (Car)
		- Two motors, one to drive and one to steer.
		- Cannot normally turn on the spot.
		- With a fixed speed and steering angle it will follow a circular path.
		- If there are four wheels, need rear differentiable and variable ('Ackerman') linkage for steering wheels.
		- Circular path of a car-like tricycle robot
			- This is a robot configuration with a single drivable and steerable back wheel. The front wheels are free running.
			- Assuming no sideways slip, we intersect the axes of the front and back wheels to form a right angle triangle, and obtain the following, where $s$ is the angle between the front and back wheels, $L$ is the distance between the front and back wheels, and $R$ is the radius of the circular motion of the front wheels of the car:
				- $$R = \frac{L}{\tan s}$$
			- The radius of the rear driving wheel is
				- $$R_d = \frac{L}{\sin s}$$
		- In time $\Delta t$, the distance driven by the robot around its circular arc is $v \Delta t$, so the angle $\Delta \theta$ through which the robot rotates is:
			- $$\Delta \theta = \frac{v \Delta t}{R_d} = \frac{v\Delta t \sin s}{L}$$

- **Odometry**
	- Robot speed - $$v = r_w \omega$$where $\omega$ = angular velocity, $r_w$ = radius of wheel

- **Actuating and Controlling Robot Wheels**
	- How do we make a wheel turn at a desired angular rate?
		- A power signal is sent to the motor (using Pulse Width Modulation - PWM).
			- This is most often a voltage signal with a fixed amplitude, but the amount of "fill in" set using Pulse Width Modulation.
		- Many real motors have built in encoders which measure their angular position.
		- For precision, encoders and feedback can be used for *servo control* using a PID Law.
	-  Feedback or servo control using an encoder
		- *Principle*:
			- Decide where we want the motor to be at every point in time
			- Check where the motor actually is at a high rate using the encoder
			- Record the difference (error)
			- Send a powed demand to the motor depending on the error, aiming to reduce it
		- Two main modes:
			- Position Control (where power demand is constant)
			- Velocity control (where power demand increases linearly with time)
		- Raw control without servo control is called power control
			- Here, the power demand is sent as a constant, programmatically
	- PID Control
		- This stands for Proportional / Integral / Differential Control
		- Error $e(t)$ is demand minus actual position
		- PID expression: sets power as a function of error: $$P(t) = k_p e(t)\ + k_i \int_{t_0}^t e(\tau)d \tau \ + k_d \frac{de(t)}{dt}$$
		- Gain constants ($k_p$, $k_i$ and $k_d$):
			- These are constants which can be tuned
			- $k_p$ - *main term* : high values give rapid response but possible oscillation
			- $k_i$ - *integral term* : can be increased to reduce steady state error
			- $k_d$ - *differential term* : can be increased to reduce settling time
		- Steady state error:
			- Steady state error is the final difference between the process variable and set point (actual angular velocity vs required angular velocity)
			- The integral term sums the error over time. The result is that even a small error term will cause the integral component to increase solwly.
			- The integral response will continually increase over time unless the error is zero, so the effect is to drive the steady-state error to zero.
		- Settling time:
			- This is the time taken by a the system to reach a steady state after a change in the set point (time taken for the error to become negligible or within an acceptable range).
			- The derivative term helps to anticipate future errors and provides a damping effect on the system's response.
			- It helps reduce overshoot and oscillations.


- **Integrating Robot Motion on a 2D Plane**
	1. Defining the position of the robot
		- Assume that a robot is confined to moving on a plane. Then, its location can be defined with a state vector consisting of 3 parameters: $$\mathbf{x} = \colv{x\\y\\\theta}$$
		- $x$ and $y$ specify the location of the pre-defined robot centre point in the world frame.
		- $\theta$ specifies the rotation angle between the two coordinate frames (the angle between the $x^W$ and $x^R$ frames)
		- The two coordinate frames coincide when the robot is at the origin and $x = y = \theta = 0$
	2. Integrating motion in 2D
		- 2D motion on a plane: 3 degrees of positional freedom, represented by ($x$, $y$, $\theta$) with $-\pi < \theta \leq \pi$.
		- Consider a robot which only drives ahead or turns on the spot:
			- *Straight line motion of distance $D$*: $$\colv{x_{new}\\y_{new}\\ \theta_{new}} = \colv{x + D\cos \theta \\ y + D \sin \theta \\ \theta}$$
			- *Pure rotation of angle $\alpha$*: $$\colv{x_{new} \\ y_{new} \\ \theta_{new}} = \colv{x \\ y \\ \theta + \alpha}$$ 
	3.  Integrating Circular Motion Estimates in 2D
		- Given the expressions for $R$ and $\Delta \theta$ for periods of constant circular motion, we can obtain: $$\colv{x_{new} \\ y_{new} \\ \theta_{new}} = \colv{x + R(\sin(\Delta \theta + \theta) + \sin \theta) \\ y - R(\cos(\Delta \theta + \theta) - \cos \theta) \\ \theta + \Delta \theta}$$
		- This works both in the case of differential drive and the tricycle robot, where we obtained the expressions for $R$ and $\Delta \theta$.



- **Position-based path planning**

- **Local and global planning with obstacles**

- define 2 coordinate frames: world frame W and robot frame R
	- robot speed v = r_w * omega (where omega (w) = angular velocity, r_w = radius of wheel)
	- DC motors:
		- power signal is sent to motor using PWM - pulse width modulation. we set the amount of power to be sent. Most often this is a voltage signal with a fixed amplitude but with the amount of 'fill-in' set using PWM
		- for precision, encoders and feedback can be used for servo control using a PID control law.
		- lego motor has encoder that records angular position. 
		- Principle: decide where we want the motor to be at every point in time. At a high rate, check where the motor actually is from the encoder. Record the difference (the error). Send a power demand to the motor depending on the error, aiming to reduce it. • Our motors: record motion rotational position in degrees. • Two main modes: position control (where demand is a constant) and velocity control (where demand increases linearly with time).
		- ![[Pasted image 20230316110956.png]]
		- ![[Pasted image 20230316111126.png]]
		- ![[Pasted image 20230316111212.png]]
		- position-based planning
			- turn to next waypoint and drive straight towards it.
			- ![[Pasted image 20230316111353.png]]
			- tan inverse can be achieved with atan2(dy, dx) in python
			- ![[Pasted image 20230316111502.png]]
		- local planning: dynamic window approach
			- robot wants to plan path around complicated set of obstacles.
			- Consider robot dynamics and possible changes in motion it can make within small time dt. 
			- For each possible motion look ahead longer time τ . Calculate benefit/cost based on distance from target and obstacles. 
			- Choose the best and execute for dt, then do it again.
			- ![[Pasted image 20230316111756.png]]
			- ![[Pasted image 20230316111909.png]]
		- Global planing: wavefront method
			- brute force 'flood fill' breadth first search of whole environment.
			- guaranteed to find shortest route, but slow
		- global planning: rapidly exploring randomised trees (RRT) method
			- Algorithm grows a tree of connected nodes by randomly sampling points and extending the tree a short step from the closest node. 
			- Expands rapidly into new areas, but without the same guarantees.