# List of exposed Functions of Virtual Driver Component:
# Category "Virtual Driver Component"

## Getters
```cpp
vdCarDrivable* GetVdCar();
```
Returns the pointer to the car of the VD. 
It refers to: 
- The controller (the VD)
- The current steer angle (rad)
- The max steer angle (rad)
- The wheelbase value (m)
- The current simulation time

```cpp
float PedalDepression();
```
Returns X the current pedals depressions. X ∈ [-1..1]. [0..1] represents acceleration from 0% to 100%, [-1..0[ represents deceleration from 0% to 100%

```cpp
float SteeringWheelAngle();
```
Returns <span style="color: red;">X</span> the current steering wheel angle. X ∈ [-1..1]. if X ∈ ]0..1] then VD steers to the right, if X ∈ [-1..0[ then VD steers to the left, from 0% to 100% off the max steering angle


## Functions

### High level - composition of low level (multiple goals added)
These functions are composition of low level function, they are more likely to be used when creating a scenario with a VD.

```cpp
void ReachSpeedInSeconds(float Speed, float TimeToReach = 0.);
```
Inputs:
- ***Speed*** (m.s-1) to maintain
- ***TimeToReach*** Time (s) to reach the desired speed

Adds the following goals to the Virtual Driver:
- Keep the current lane
- Reach ***Speed*** in ***TimeToReach*** seconds
	
```cpp
void FollowCar(const UVirtualDriverComponent* LeadCar, float Headway = 1.6);
```
Inputs:
- ***LeadCar*** Car to follow
- ***Headway*** Time headway (s) to maintain, default value = 1.6s

Adds the following goals to the Virtual Driver
- Keep the current lane
- Follow ***LeadCar*** at the given Time ***Headway***

```cpp
void ReachSpeedInMeters(float Speed, float TotalDist, bool IsInfinite = true);
```
Inputs:
- ***Speed*** (m.s-1) to maintain
- ***TotalDist*** Distance (m) to reach ***Speed***
- ***IsInfinite*** specify if the goal end when speed is reached, or will never end.

Adds the following goals to the Virtual Driver
- Keep the current lane
- Reach ***Speed*** in ***TotalDist*** distance, maintain afterwards it if ***isInfinite***

```cpp
void ChangeLane(int Lane, float S, float Speed, float BezierIn = 25., float BezierOut = 25.);
```
Inputs:
- ***Lane*** offset to apply (-1: one lane on the left, +1 one lane on the right, -2 two lanes on the left)
- ***S*** Time (s) to reach the new lane
- ***Speed*** (m.s-1) to reach at the end of the lane change
- ***BezierIn*** start control point distance ([0..100]) of the Bezier curve. Vector is aligned with previous trajectory 
- ***BezierOut*** end control point distance ([0..100]) of the Bezier curve. Vector is aligned with future lane

Adds the following goals to the Virtual Driver
- Change to ***Lane*** direction, then keep the new lane
- Reach ***Speed***, then maintain it

```cpp
void CrossJunction(int Strategy, float SpeedBefore, float SpeedAfter, bool isImmediate = true);
```
Inputs:
- ***Strategy*** is where the VD will turn in the junction. List of strategies:
    - LEFT_SECOND = -2,
	- LEFT_FIRST = -1,
	- STRAIGHT = 0,
	- RIGHT_FIRST = 1,
	- RIGHT_SECOND = 2
- ***SpeedBefore*** to reach before the beginning of the junction
- ***SpeedAfter*** to reach after the end of the junction
- ***isImmediate***  

Adds the following goals to the Virtual Driver
- Reach ***SpeedBefore*** before the junction
- Follow the road in the junction that correspond to the ***Strategy***
- Reach ***SpeedAfter*** during the junction
- Keep the lane connected to the ***Strategy***'s road after the junction

### Low level - Only one goal (lateral xor longitudinal)
These function are basic element allowing creation of more understandable function (more high level). 
Nevertheless, they can also be called.

```cpp
void AddGoalLatTrajOdrJunction(int Strategy, bool isImmediate = true);
```
Inputs:
- ***Strategy*** 
- ***isImmediate*** 

Adds the following goals to the Virtual Driver
- Follow ***Strategy*** for the next junction

```cpp
void AddGoalLatTrajOdr(bool isImmediate = true);
```
Inputs:
- ***isImmediate*** 

Adds the following goals to the Virtual Driver
- Follow the current lane endlessly (till next junction)

```cpp
void AddGoalLatTrajBezier(const UOpenDriveComponent *Start, const UOpenDriveComponent *End, float CpStart = 50., float CpEnd = 50., bool isImmediate = true);
```
Inputs:
- ***Start*** Opendrive point in environment that define the starting point of the Bezier curve
- ***End*** Opendrive point in environment to end the Bezier curve
- ***CpStart*** control point of the starting point of the Bezier curve
- ***CpEnd*** control point of the ending point of the Bezier curve
- ***isImmediate*** 

Adds the following goals to the Virtual Driver
- Add a Bezier curve to follow regarding two opendrive points

```cpp
void AddGoalLongReachTime(float Speed, float TimeToReach = 0., bool isInfinite = true, bool isImmediate = true);
```
Inputs:
- ***Speed*** to reach
- ***TimeToReach*** time to reach ***Speed***
- ***isInfinite*** specify if the goal end when speed is reached, or will never end.
- ***isImmediate*** 

Adds the following goals to the Virtual Driver
- Reach ***Speed***, maintain afterwards it if ***isInfinite***

```cpp
void AddGoalLongReachDistance(float Speed, float DistToReach = 0., bool isInfinite = true, bool isImmediate = true);
```
Inputs:
- ***Speed*** to reach
- ***DistToReach*** to reach ***Speed***
- ***isImmediate***

Adds the following goals to the Virtual Driver
- Reach ***Speed*** in ***DistToReach*** meters


```cpp
void AddGoalLongMaintain(float Speed, bool isImmediate = true);
```
Inputs:
- ***Speed*** to maintain
- ***isImmediate*** 
Adds the following goals to the Virtual Driver
- Maintain ***Speed***

### Data computation

```cpp
float RoadDistanceTo(const UVirtualDriverComponent* Other);
```
Inputs:
- ***Other*** the targeted positionable in the current opendrive

Returns:
- Distance in track position (S), bumper to bumper


```cpp
float THW(const UVirtualDriverComponent* Other);
```
Inputs:
- ***Other*** the targeted mobil in the current opendrive

Returns:
- Time headway between the two mobil


```cpp
float TimeTo(const UOpenDriveComponent* Other);
```
Inputs:
- ***Other*** the targeted mobil in the current opendrive

Returns:
- Time to reach the ***Other*** mobil (at current speed)


```cpp
float TTC(const UVirtualDriverComponent* Other);
```
Inputs:
- ***Other*** the targeted mobil in the current opendrive

Returns:
- Time to Collision to the ***Other*** mobil


```cpp
float ETTC(const UVirtualDriverComponent* Other);
```
Inputs:
- ***Other*** the targeted mobil in the current opendrive

Returns:
- Enhanced Time to Collision (ISO 22839) to the ***Other*** mobil



# List of exposed Properties of OpenDrive Component:

## Category "OpenDRIVE"
```cpp
int RoadId;
```

```cpp
int LaneId;
```

```cpp
float S_;
```

```cpp
float T_;
```

```cpp
float H_;
```

# List of exposed functions of the Virtual Driver:
## Category = "OpenDRIVE"
```cpp
void GetPosition();
```

```cpp
void SetPosition();
```

## Category = "OpenDrive Component"
```cpp
void SetTrackPosition(int track_id, int lane_id, float s, float offset, float h);
```

```cpp
bool MoveAlongS(float S, int Strategy=0);
```

```cpp
int GetRoadId();
```

```cpp
int GetJunctionId();
```

```cpp
float GetNextJunctionDistance();
```

```cpp
float GetNextJunctionId();
```

```cpp
bool IsJunctionDistanceLessThan(float Dist, int JunctionId = -1);
```

```cpp
float SDistanceTo(const UOpenDriveComponent* Other);
```

```cpp
float GetCurrentCurvature();
```

```cpp
float GetNextCurvature(float dist) const;
```