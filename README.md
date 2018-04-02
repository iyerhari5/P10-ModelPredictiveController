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

# Implementing the Model Predictive Controller
The code for the MPC is implemented in MPC.cpp. 

# Effect of the different parameters
The parameters were optimized manually trying out different parameters. Kp is proportional to the error term. Intuitively, a high value here causes the 
car to overshoot the target and causes wild oscillations. This was set to -0.09. The Kd term corrects for the overshoot and was set to -0.50. This gave
satisfactory results with the simulator. The integral term is usually used to correct for bias (such as a misaligned front wheel).  The integral term was set to 
-0.001 in the final implementation. Please note that these values could change with the simulator resolution and speed of the system. 

# Results

The [video](https://youtu.be/rfUnKe-pWJw) shows the performance the PID controller on the simulator track.

