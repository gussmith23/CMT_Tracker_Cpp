# CMT_Tracker_Cpp
CMT Tracking in C++. Based on Nebehay's CMT. Original C# code by Josh Snyder of Penn State's Microsystems Design Lab. Josh's code here: [C# repo link.](https://github.com/gussmith23/CMT_Tracker)

# Structure
- Delegates
  - External SURF Descriptors
  - External SURF Keypoints (one or both of these will be handled by OpenSURF)
  
- Class `CMT`
  1. `Initialize(frame, ROI)`
    - We extract keypoints from entire frame using SURF, and then we split them into object and background pts by whether or not they fall into the ROI.
    - Given that there are object keypoints, we extract SURF descriptors using SURF.
    - Given that there are background keypoints, we extract SURF descriptors likewise. (note that descriptors are called features interchangeably.)
    - Each keypoint is given a class. Object keypoints are given unique classes 1, 2, 3, etc., while background keypoints are all 0.
    - All features are collected into one matrix, as with all keypoints.
    - Distance between object keypoints is computed.
    - Lastly, a region for updating all of the important members of `CMT_SURF`.
  2. `Process(frame, ROI)` --> returns new ROI, but also sets `Valid` flag.
    - Call to `Track`
    - Call to `Estimate`
    - Match newly detected keypoints to all keypoints.
    - Match newly detected keypoints to object keypoints given that object exists.
    - Do the same with the adaptive model (not sure what this is yet).
    - Stopped at ln 1221, which seems to be an important section. Continue there when you pick up next time.
