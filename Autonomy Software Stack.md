# Proposal: Restructuring Our Approach to Building the Self-Driving Car

## 🧭 Summary

We’ve made progress across perception, world modelling, and action modules—but we’re stretched too thin. We’re solving many advanced problems simultaneously without a working base system to unify the work. 

This proposal lays out a simpler, more structured approach:  
**Build a car that can navigate from Point A to Point B in an open lot while detecting and avoiding obstacles.**

Achieving this gives us a functioning "robot", a platform to test other modules, and a concrete milestone to build on. It also gives new members a clear direction.

I know this has been the goal from the start but I don't think our team has the synery right now to understand how exactly we plan on executing this. Maybe Eddy had a solid grasp on how the plan should be executed but It's a little overwhelming trying to hit self driving all at once. My biggest concern right now is that we don't have much to show and I'd like for Eve to have something to put out there.


---

## 🚗 Term Goal

> **Build a robot car that drives from Point A to Point B while avoiding static (maybe dynamic) obstacles (e.g., cones, pedestrians).**

This is a classic navigation stack problem and does *not* require HD maps, semantic understanding of traffic lights, or dynamic traffic rules. It’s the foundational behavior of an autonomous system.

---

## ❌ Current Problems

- **Team is fragmented**: Members are working on advanced modules without a shared integration goal.
- **No unifying stack**: We have detection, mapping, and control systems in isolation, but no way to test them on a functioning robot.
- **Too many features at once**: We’re tackling lane keeping, 3D tracking, HD mapping, and more, without a baseline system.
- **No tangible output**: Despite great work, we can’t currently demo anything end-to-end.It would be great to show the car in motion

---

## ✅ Proposed Phased Approach

Break the autonomous stack into **phases**, starting with basic functionality.

### **Phase 1: Lot Navigation System**
- Car drives from point A to B in an open lot
- Detects and avoids obstacles (cones, pedestrians, vehicles)

Once Phase 1 is complete, we move to:
- **Phase 2**: Lane keeping and structured road following
- **Phase 3**: Traffic light and sign handling
- **Phase 4**: Full AV-level autonomy with routing and dynamic road rules

> **This is a very rough approach to phases but just an idea for you to unterstand how I'm thinking about approaching this. Below is my implementation of Phase 1**
---

## 🧱 Proposed Stack for Phase 1


### 1 . **Perception**

**Obstacle Detection:**
- YOLOv8 on 3-camera views (front, left, right or stitched)
- Outputs bounding boxes for obstacles (cars, people, cones)

**Depth Estimation:**
- **Below are just ideas but to keep it simple we should stick with just using LiDAR as the main source of depth and spatial awareness**
- If stereo: Use OpenCV + ELAS/SGBM
- If monocular: Use Monodepth2, DPT, or Midas
- If LiDAR: Use directly or fuse with camera detections 

**(Optional)** Semantic Segmentation:
- Use DeepLabV3+ or YOLO-Seg to label drivable vs non-drivable regions
---
### 2. **Localization**

**Primary:**
- RTK GPS + IMU + Wheel Odometry
- Fuse using `robot_localization` or a custom EKF

**Backup (for GPS drift):**
- Visual-Inertial Odometry (VIO)
  - Options:
    - [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion)
    - [OpenVINS](https://github.com/rpng/open_vins)
    - [ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3)

---

### 3. **Mapping & Costmaps**

**Local Costmap:**
- Inputs:
  - Real-time LiDAR
  - Detected obstacles projected into local frame
- Use `nav2_costmap_2d` or `grid_map`
- Resolution: ~0.1–0.2m

**Global Map (optional):**
- If reusing the same parking lot:
  - Map once using LIO-SAM or Cartographer
  - Localize with AMCL or scan matching
  - Otherwise, GPS-only navigation suffices

---

### 4. **Path Planning**

**Global Planner:**
- Waypoint navigation using GPS → map frame conversion
- Use Nav2 global planner or custom A*

**Local Planner:**
- Use TEB (Timed Elastic Band) or Pure Pursuit
- Inputs:
  - Local costmap
  - Goal pose

---

### 5. **Control**

- Use `ackermann_msgs` if Ackermann steering
- Or convert to `cmd_vel` for diff-drive
- Tune PID for now, explore MPC later

---

## 🧑‍💻 Core Leads Team for Phase 1

To build and integrate the stack efficiently, we need the people below to all be on the same page and understand what the goal is. Everyone agrees that our goal should be way point autonomy (so we have a map, place a marker, and the car drives from point A to point B) but because we're spread so thin, everyone ends up working on individual tasks without any synergy or plans for integration. My biggest concern for this term and the future of Eve is the lack of integration between modules (perception, world modelling, action) and I think we've definitely tried to create more synergy between teams by hosting **autonomous software** syncs but I have a feeling that people are still overwhelmed by the sheer amount of work there is to do. That's why I'm proposing to keep it simple and aim to **solve a simple navigation problem with a real car**. We can think of this as just making a giant robot navigate from point A to point B. 

- **Kishore**
- **Hasan**
- **Lucas**
- **Brian**
- **Helen**
- **Jaden**
- **Stephen**
- **Vishal**

This group would focus on getting a full end-to-end system working. What this means to me is that every single member listed above has a clear idea of what our goal is. As listed above in **Phase 1**, we are aiming to solve a significantly more simplified problem. 

The reason why I'm propsing this is because I've come to realize how well the other teams function and get things done. One major advantage they have over Eve is that fact that their teams are small and they are solving a relatively simpler problem than  attempting to solve **self driving** all at once. 

- **Humanoid**: Control Robot Arm with VR (not simple but multiple people on the team have a very solid understanding of the entire stack)
- **Rover**: Navigate a robot from point A to B while avoiding obstacles
- **F1 Tenth**: F1 tenth has an entire course that teaches them how to build the car which makes it great but they also have a smaller team so everyone is on the same page. Their goal is also simpler than building a self driving car all at once (Running SLAM for navigation)

The common denominator here is that they have smaller teams, everyone is on the same page, and the problem the goal the team has to acheive is realistic in terms of difficulty.

I feel this is something Eve lacks which is **definitely something I should be held accountable for. I do believe its up to us as captains to create this synergy. We should foster an environment where realistically, any one of the directors could be captains.** 


---

## 🌱 How This Includes the Whole Team

We still have a large and passionate team.

- Other members should continue working on submodules like:
  - HD mapping
  - 3D tracking
  - Depth estimation
  - Advanced perception (e.g., traffic lights, signs)
  - 2D to 3D
- These modules can be cleanly plugged into the working robot
- Everyone will be able to test, deploy, and see their work in action
- Eddy's vision has always been (or what I believe it is) to create a working self driving car and having future students use it for research
    - If someone wants to try a new algorithm, they can turn on the car and test it out with a base "robot" that already has basic navigation
    - My response to this is "why not aim for that right now?" Let's enable the car to be able to acheive basic navigation and slowly begin implementing the other features which make a self driving car
    - After acheiving basic navigation, we can move on to **lane keeping**, and then **traffic sign/light handling**, etc.

---

## 🛠 Why a Fresh Repo?

- Clear scope: Strip to the essentials
- Clear documentation and responsibilities
- Avoid overhead of mono-repo until core stack is complete
- Focus on building something we can **demo and iterate on**

> **This is very much up for discussion. I don't think its necessary. I feel like the current monorepo was designed with full self driving in mind (which is great) but maybe there's an easier approach to this? This point isn't necessary at all**
---

## 🧠 Closing Thoughts

Right now, we don’t have a functioning robot to show, despite all the work we’ve done. That needs to change. If we can get this basic navigation stack working this term, we will have:

- A minimal viable autonomous system
- A clear integration pathway for all modules
- A working testbed for future contributors

I think tackling a simpler problem of navigation instead of trying to take on full self driving head on is a lot more motivating. I like to think of this as building one big robot with basic navigation (kind of like the ASD assignment). We have all the tools to be able to this. I just think its time we approach this with a bit more structure much like the other teams WATonomous has. 

We all have the same fundamental idea of trying to get this Car to go from point A to point B autonomously. I feel like we're just approaching it with our ideas spread too thin which leads to minimal productive work. I feel that many of us might benefit from feeling more in control of the overall direction of Eve.


Let me know your thoughts.

**– Kishore**




[[Perception]]
[[World Modelling]]
[[Controls]]
[[Machine Learning]]