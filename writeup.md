# Introduction
The goal of this project is to implement MPC algorithm, to drive the car in a track.

# Model description
The model uses the status of the car and the way points, to calculate actuators. The status includes the location x,y, the speed, the car direction. The actuators are the throttle and the steering angle. 

The waypoints are fit into a 3rd order polynomial. This is used to calculate the cte, and epsi values to be used later in the optimization algorithm.

The optimization algorithm takes cte and epsi as input, alnogside some parameters to prevent the vehicle from stopping, and to prevent the vehicle from harsh steering or harsh acceleration. The weights for these factors are chosen based on trial. 

## dt and N
dt was set to 0.1, and N to 10. It means the model will predict 1 second ahead, which is reasonably good enough, and will not consume a lot of processing power. If N is set larger, the model will produce new delay, and will not be able to keep up with the simulator, and the car will drive off track.

## Polynomial Fitting and MPC Preprocessing

Waypoints are fitted into a 3rd order polynomial. Before fitting, the points reference is converted from the map reference, to the vehicle reference. 

## Model Predictive Control with Latency
To resolve the latency, the model uses the location and the speed values predicted after 100 ms. To predict these values, the same equations used in the MPC model are used. The result of the prediction is used as the state vector passed to the MPC model. The vehicle current acceleration and steering is used to predict the state in 100 ms up front.
