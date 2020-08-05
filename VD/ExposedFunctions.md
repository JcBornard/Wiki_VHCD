# List of exposed Functions of Virtual Driver Component:
# category = "Virtual Driver Component"
```cpp
vdCarDrivable* GetVdCar()

float PedalDepression()

float SteeringWheelAngle()

void ReachSpeedInSeconds(float Speed, float TimeToReach = 0.);

void FollowCar(const UVirtualDriverComponent* LeadCar, float Headway = 1.6);

void ReachSpeedInMeters(float Speed, float TotalDist, bool IsInfinite = true);

void ChangeLane(int Lane, float S, float Speed, float BezierIn = 25., float BezierOut = 25.);

void CrossJunction(int Strategy, float SpeedBefore, float SpeedAfter, bool isImmediate = true);

void AddGoalLatTrajOdrJunction(int Strategy, bool isImmediate = true);

void AddGoalLatTrajOdr(bool isImmediate = true);

void AddGoalLatTrajBezier(const UOpenDriveComponent *Start, const UOpenDriveComponent *End, float CpStart = 50., float CpEnd = 50., bool isImmediate = true);

void AddGoalLongReachTime(float Speed, float TimeToReach = 0., bool isInfinite = true, bool isImmediate = true);

void AddGoalLongReachDistance(float Speed, float DistToReach = 0., bool isInfinite = true, bool isImmediate = true);

void AddGoalLongMaintain(float Speed, bool isImmediate = true);

float RoadDistanceTo(const UVirtualDriverComponent* Other);

float THW(const UVirtualDriverComponent* Other);

float TimeTo(const UOpenDriveComponent* Other);

float TTC(const UVirtualDriverComponent* Other);

float ETTC(const UVirtualDriverComponent* Other);
```


# List of exposed Properties of OpenDrive Component:
## Category = "OpenDRIVE"
```cpp
int RoadId;

int LaneId;

float S_;

float T_;

float H_;
```

# List of exposed functions of the Virtual Driver:
## Category = "OpenDRIVE"
```cpp
void GetPosition();

void SetPosition();
```

## Category = "OpenDrive Component"
```cpp
void SetTrackPosition(int track_id, int lane_id, float s, float offset, float h);

bool MoveAlongS(float S, int Strategy=0);

int GetRoadId();

int GetJunctionId();

float GetNextJunctionDistance();

float GetNextJunctionId();

bool IsJunctionDistanceLessThan(float Dist, int JunctionId = -1);

float SDistanceTo(const UOpenDriveComponent* Other);

float GetCurrentCurvature();
```