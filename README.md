## Running the Code
This project involves the Term 2 Simulator which can be downloaded [here](https://github.com/udacity/self-driving-car-sim/releases)

This repository includes two files that can be used to set up and intall uWebSocketIO for either Linux or Mac systems. For windows you can use either Docker, VMware, or even Windows 10 Bash on Ubuntu to install uWebSocketIO.

Once the install for uWebSocketIO is complete, the main program can be built and ran by doing the following from the project top directory.

1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./mpc

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)


[image1]: ./Images/mpc-model.png
[image2]: ./Images/Run3.gif

# Model Predictive Controller
Model Predictive Controller (MPC) frames the task of following a trajectory as an optimization problem. MPC simulates different actuator inputs and 
computes the resulting trajectories. The trajectory with the least cost is selected as the output. At each time instant, the current state and the
reference trajectory are known. The MPC optimizes the actuator inputs such that the cost is minimized. From the resulting actuator outputs, the first
set of actuator commands are executed and the rest are thrown away. This process is repeated at each time instant.

# The Model

The motion model used is shown below:

![alt text][image1]

# Timestep Length and Elapsed Duration (N & dt)
I experimented with various values of N & dt pairs such as (N=10, dt = 0.1), (N=20, dt=0.1) etc. However the final values that showed reasonable 
performance was N = 12 and dt = 0.05. This means the MPC is predicting 600 ms into the future.


# Polynomial Fitting and MPC Preprocessing
The way points from the simulator are in global coordinates. First they are converted to the car coordinate frame. Hence the car position is assumed 
to be at (px,py,psi) = (0,0,0). 

# Model Predictive Control with Latency

The main challenge in this project was to allow for 100ms in latency from the current time instant to when the actuator inputs would be effective.
The approach used to handle this was to do the trajectory prediction into the future, and then apply the actuator values from the time point after
the latency period. In our case N=12 and dt = 0.05. So in order to account for 0.1 second latency, we use the 3rd set of actuator values returned from
the optimizer to actuate the car.  In order for this to work, we also have to constraint the actuator values to the current actuator values for 
the period of the latency. See MPC.cpp lines 13-16 ,200-205 and 215-220. 


# Results

The video below shows the performance of the MPC on the simulator.
![alt text][image2]

