#Description

The Virtual Driver (VD) is a software driving a car inside an opendrive description (xodr).
VD controls the car through steering wheel angle and pedal depression.
Controlled car is connected to the VD through a virtual class that must be implemented in the welcoming simulator.

# Internal components
at a given simulation time, VD as:
- Current lane: the opendrive's drivable lane that VD can project into
- Current speed: the current speed of the controlled car

- Current pedals depression: the current computed pedals depression allowing VD to reach the desired speed
- Current steering wheel angle: the current computed angle of the steering wheel allowing VD to maintain the car close to the desired trajectory

- Current speed goal: the speed that VD need to reach and/or maintain
    - This is a **longitudinal goal**
- Current trajectory: the trajectory that VD currently maintain. This can be the center of a lane, or a custom Bezier curve
    - This is a **lateral goal**

- A list of chained longitudinal goals
- A list of chained lateral goals


# Use
Once the VD is connected to a simulated car and an opendrive file is provided to it, then it become possible to place the simulated car holding the VD in the simulation

If the car is placed on a lane, then this lane become natively the current lane to follow. This define automatically the current longitudinal goal

