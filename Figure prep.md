- look deeper test theory
- no correct way to do cicd for robotics
- test automation with simulation -> upside(any scenario) /  downslide(accuracy to real life, lots of compute)
- replay testing -> record real life data, NAS (big drive to connect to over the network), 
- ros not deterministic problems -> 90% pass rates -> how to reduce this
- building -> how to rebuild the code in the most efficient way possible -> adding minutes to everyone's CI will cost millions over a year -> cache, only building when needed (docker caching, compiler level caching (colcon build level)) 
- look into docker caching https://docs.docker.com/build/concepts/dockerfile/

CI/CD: 
- Sourcing (git commits)
- Static Analysis (linting)
- Building (docker, cmake)
- Unit Testing (pytest, gtest)
- Integration Tests (ROS launch files + pytest)
- Simulation / Replay /  HIL Tests 
- Artifact Packaging (wraps builds for delivery) (pushing docker image to registry)
- Deployment (OTA's, AWS, Ansible)
- Some sort of monitoring system (grafana -> Prometheus)
- logging (testrail, jira)
- Orchestration tools (Github Actions, Jenkins, Gitlab)

Types of tests:
- Unit tests
- Integration tests (planner + controller working)
- Simulation tests (entire stack)
- Replay tests (play real rosbag into stack)
- HIL / Full system tests


✅ **Day 1: Foundations & Core Technical Skills**

#### ⏰ Morning (3–4 hours) — **Python, C++, and Linux**

- **Python**:
    - Write automation scripts using `unittest`, `pytest`, `argparse`, and `os`.
    - Practice parsing and managing structured data: `json`, `csv`, and file I/O.    
    - Review subprocess handling for test automation.
        
- **C++**:
    - Focus on memory management, pointers, classes, and templates.
    - Practice debugging using `gdb`.
    - Understand makefiles and basic build systems (tie-in to Bazel).
        
- **Linux**:
    - Shell scripting (basic bash): loops, conditions, file manipulation.
    - Navigating Linux file systems, `top`, `ps`, `dmesg`, and `journalctl`.
    - Permissions, services (`systemd`), and device files.
        

#### ⏰ Afternoon (3 hours) — **Test Automation & CI/CD**

- Understand test types: unit, integration, system, regression.
- Learn how CI/CD works:
    - Tools like GitHub Actions, GitLab CI, Jenkins.
    - YAML file syntax for pipelines.
    - How Docker is used in testing environments.
- Try automating a small pipeline with GitHub Actions or GitLab CI if you can.
    

#### ⏰ Evening (1–2 hours) — **Embedded Systems & Communication**

- Review communication protocols:
    - **CAN**: frame structure, arbitration, debugging with candump.
    - **Serial, USB, Ethernet, EtherCAT** basics.
- Study basic computer architecture:
    - RAM/ROM, cache hierarchy, instruction sets, memory-mapped I/O.
        

---

### ✅ **Day 2: Hands-On Practice & Interview Simulation**

#### ⏰ Morning (3–4 hours) — **Project-Based Review**

- Build a mock project:
    - Write Python scripts that simulate sensor data collection.
    - Use Python to automate tests on dummy firmware responses.
    - Set up a basic `Dockerfile` for a test environment.
- Use lab instrument simulators or YouTube demos to understand:
    - **Oscilloscope** basics (triggering, voltage/time axes).
    - **Logic analyzer** workflows (timing analysis, decoding).

#### ⏰ Afternoon (2–3 hours) — **Mock Interview Practice**

- Prepare to explain:
    - A past hardware/software project, including testing methodology.
    - Your debugging workflow when a sensor or communication line fails.
    - How you’d write a script to test multiple robot calibration cases.
- Practice answering:
    - “How would you design a test plan for a humanoid’s motor controller?”
    - “How would you integrate test results into a CI/CD pipeline?”

#### ⏰ Evening (1–2 hours) — **Bonus & Review**

- Review:
    - Docker: container vs. VM, Dockerfile basics, mounting volumes.
    - Bazel: high-level architecture, advantages over Make.
- Light review or flashcards for:
    - Communication protocols.
    - C++ syntax quirks (e.g., object slicing, virtual destructors).