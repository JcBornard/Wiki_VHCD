# List of exposed Functions of Virtual Driver Component:
# Category = "Virtual Driver Component"
```cpp
vdCarDrivable* GetVdCar();
```

```cpp
float PedalDepression();
```

```cpp
float SteeringWheelAngle();
```

```cpp
void ReachSpeedInSeconds(float Speed, float TimeToReach = 0.);
```

```cpp
void FollowCar(const UVirtualDriverComponent* LeadCar, float Headway = 1.6);
```

```cpp
void ReachSpeedInMeters(float Speed, float TotalDist, bool IsInfinite = true);
```

```cpp
void ChangeLane(int Lane, float S, float Speed, float BezierIn = 25., float BezierOut = 25.);
```

```cpp
void CrossJunction(int Strategy, float SpeedBefore, float SpeedAfter, bool isImmediate = true);
```

```cpp
void AddGoalLatTrajOdrJunction(int Strategy, bool isImmediate = true);
```

```cpp
void AddGoalLatTrajOdr(bool isImmediate = true);
```

```cpp
void AddGoalLatTrajBezier(const UOpenDriveComponent *Start, const UOpenDriveComponent *End, float CpStart = 50., float CpEnd = 50., bool isImmediate = true);
```

```cpp
void AddGoalLongReachTime(float Speed, float TimeToReach = 0., bool isInfinite = true, bool isImmediate = true);
```

```cpp
void AddGoalLongReachDistance(float Speed, float DistToReach = 0., bool isInfinite = true, bool isImmediate = true);
```

```cpp
void AddGoalLongMaintain(float Speed, bool isImmediate = true);
```

```cpp
float RoadDistanceTo(const UVirtualDriverComponent* Other);
```

```cpp
float THW(const UVirtualDriverComponent* Other);
```

```cpp
float TimeTo(const UOpenDriveComponent* Other);
```

```cpp
float TTC(const UVirtualDriverComponent* Other);
```

```cpp
float ETTC(const UVirtualDriverComponent* Other);
```


# List of exposed Properties of OpenDrive Component:
## Category = "OpenDRIVE"
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