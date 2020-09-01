# Description

The Virtual Driver (VD) is a software driving a car inside an opendrive description (xodr).
Management of the opendrive file is done using [esmini](https://github.com/esmini/esmini) parser & functionnalities. 
This parser creates an accessible road network description system from the .xodr file,
and provides useful features for the VD to use (e.g. Euclidian positioning to track positioning and vice versa)

VD controls the car through steering wheel angle and pedal depression.

Controlled car is connected to the VD through a virtual class that must be implemented in the welcoming simulator.

# Internal components
At a given simulation time, VD has:
- Current lane: the opendrive's drivable lane that VD can project into
- Current speed: the current speed of the controlled car

- Current pedals depression: the current computed pedals depression allowing VD to reach the desired speed
- Current steering wheel angle: the current computed angle of the steering wheel allowing VD to maintain the car close 
to the desired trajectory

- Current speed goal: the speed that VD need to reach and/or maintain
    - This is a **longitudinal goal**
- Current trajectory: the trajectory that VD currently maintain. This can be the center of a lane, or a custom Bezier curve
    - This is a **lateral goal**

- A list of chained longitudinal goals
- A list of chained lateral goals


# VD use
Once the VD is connected to a simulated car and an opendrive file is provided, 
then it become possible to place the simulated car holding the VD in the simulation.

If the car is placed on a lane, then this lane become natively the current lane to follow. 
This define automatically the current longitudinal goal
If not, then the car will try to reach the closest drivable lane.

Default speed of the VD car, the default longitudinal goal, is set  overcome to 0m/s.
To trigger the movement of the car, it is needed to add a non nul longitudinal goal.

# Goals
VD's goals are what it will try to follow, a speed command (longitudinal) or a path (lateral).
A goal can be infinite (e.g. a speed to follow, a lane to follow), or physically constrained 
(e.g. a path to lane change, a speed to reach in less than X meters).
The VD has two goal lists: (i) the longitudinal list and (ii) the lateral list.

To add something to a list, most of the function of the VD have a "isImmediate" boolean parameter. 
"True" mean that the provided goal will overwrite the current goal and the VD will immediately try to achieve the new goal.
"False" mean that the provided goal will be filled to the list.

## Longitudinal goals list
This list contains each chained longitudinal goals that are provided to the VD.
A default goal is always set, as the last speed to be maintained.


## Lateral goals list



 
