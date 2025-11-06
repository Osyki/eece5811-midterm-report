# EECE5811 - Midterm Report

## Project Design

### System Overview

The project is designed to evaluate the performance of a deep learning-based scheduling algorithm against traditional scheduling algorithms in a simulated real-time operating system (RTOS) environment. The simulated RTOS reads in a set of tasks (called a workload) with varying parameters and passes them to the scheduling algorithms. Additional details of the workload and task parameters are defined [here](#workload-and-task-parameters). The DL algorithm optimizes for performance metrics that include deadline miss rate, average response time, CPU utilization, context switch overhead, and number of preemptions. The following scheduling algorithms are currently being implemented for comparison:

- ✔️ Earliest Deadline First (EDF)
- ✔️ Fixed Priority Scheduling (FPS)
- ✔️ Round Robin (RR)
- ➖ Deep Learning-based Scheduling (DL Scheduler)
- ❌ Rate Monotonic Scheduling (RMS)
- ❌ Preemptive Priority Scheduling (PPS) with Aging

### <a name="system-architecture">System Architecture</a>

The system architecture consists of the following key components:

1. **Workload Generator**: Generates workloads with varying task characteristics.
    - Each task is defined by parameters such as:
        - task ID
        - task type (periodic, aperiodic, sporadic)
        - arrival time
        - execution time
        - worst-case execution time (WCET)
        - deadline
        - period (if periodic)
        - priority (if applicable)
        - criticality level (if applicable)
2. **Scheduler Implementations**: Contains the logic for each scheduling algorithm, including the DL-based scheduler that utilizes a neural network for task selection.
    - Each scheduler inherits from a base `BaseScheduler` class and implements a `select_task()` method to determine which task to run next.
3. **Simulation Engine**: Simulates the RTOS environment, executing tasks according to the selected scheduling policy and collecting performance metrics.
    - Responsible for managing the execution context, including task states (ready, running, blocked) and scheduling decisions.
4. **Evaluation Module**: Analyzes the collected data, generating reports and visualizations to compare the performance of the different scheduling algorithms.
    - Computes metrics such as deadline miss ratio, average response time, CPU utilization, context switches, and preemptions.
    - Utilizes SciPy and Matplotlib for statistical analysis and visualization.
5. **Training Module**: Implements the training pipeline for the DL scheduler using the fast.ai library, including model architecture, training routines, and hyperparameter tuning.

### Component Interactions

- The `Workload Generator` creates a set of tasks that are fed into the `Simulation Engine`.
- The `Simulation Engine` reads the workload and processes all tasks through the implemented schedulers, including the `DL scheduler`.
- The `Scheduler Implementations` are invoked by the `Simulation Engine` to process task scheduling.
- The `Evaluation Module` collects performance data during simulation and generates reports.
- The `Training Module` is used to train the DL scheduler model prior/during simulation runs.


## Milestones

### Achieved
- Have learned (and continuing to learn) the fast.ai library for DL model implementation.
- Implemented basic RTOS simulation framework with task management.
- Identified and implemented parameters and data structures for task representation.
- Implemented traditional RTOS scheduling algorithms:
    - Earliest Deadline First (EDF)
    - Fixed Priority Scheduling (FPS)
    - Round Robin (RR)
- Developed initial version of the DL-based scheduler.
- Developed workload generator for various task types.

### Planned
- Implementation of Preemptive Priority Scheduling (PPS) with Aging.
- Implementation of Rate Monotonic Scheduling (RMS).
- Complete training pipeline for DL scheduler. (Might have to pivot to PyTorch since fast.ai has some limitations)
- Comprehensive evaluation module with statistical analysis and visualization.
- Extensive testing with mixed workloads and varying system conditions.
- Documentation and final report preparation.
- **Stretch Goal**: Explore implementation of multi-core scheduling support. 

### Questions

#### If you are implementing something, why did you choose a particular language/framework? What works? What doesn’t work?

I chose Python for its extensive libraries and ease of use in both simulation and deep learning tasks. The fast.ai library was initially selected because it offered a high-level API for building and training deep learning models quickly. However, I have encountered some limitations with fast.ai in terms of flexibility and control over model architecture, which has lead me to consider using PyTorch directly for more complex implementations. Specifically, fast.ai's abstractions cause additional overhead/limitations when implementing custom training loops or structures. This has made debugging and fine-tuning more challenging than anticipated.

#### Did you meet your milestone? If not, what made you fail to achieve it?

I have met most of my initial milestones. The priority for the midterm report was to implement an early version of the DL algorithm using the fast.ai library and a basic RTOS simulation framework. While I have successfully implemented traditional scheduling algorithms (EDF, FPS, and RR), I have not yet completed the DL scheduler training pipeline. I have an initial version of the DL scheduler working, but it requires additional tuning and testing (especially since I might pivot from fast.ai to PyTorch). The main challenge evolves from the lack of comprehensive understanding of building DL algorithms with no prior knowledge. Additionally, time constraints and ensuring the accuracy of the various scheduling algorithms under various conditions contributed to delays.

#### Did you encounter any challenges? How did you solve it?

Yes, as mentioned above I faced challenges with learning the fast.ai library due to high-level abstractions and found difficulties during the implementation of the DL algorithm. This includes difficulty in modifying the underlying architecture in a fast.ai model (fast.ai requires specific data formats and structures to be passed as parameters) and learning how to properly retrain an existing model with a new dataset. To address this, I have been exploring PyTorch as an alternative, which provides more granular control over model architecture and training processes. 

#### Do you need to change your milestones (for final report/presentation) promised in your initial report? If yes, justify your reasons.

Yes, I have made adjustments and added more details to the milestones as outlined above. This is primarily due to the feedback I received in the initial report. I realize that the initial milestones were too high-level and lacked specific details regarding the implementation of each component. 

Additionally, I am removing the use of the rt-app framework for simulation as it adds unnecessary complexity since I do not have prior experience with both DL and the rt-app. I believe learning an additional framework would detract from the core objectives of the project. Instead, I have built a simple RTOS simulation engine, which allows for additional time and understanding of the scheduling algorithms being implemented.

I am also not attempting kernel integration for the DL scheduler at this time, as it would require significant additional effort and time to implement and test. The focus will remain on simulation and evaluation within a controlled environment. If I complete the core objectives ahead of schedule, I may explore multi-core scheduling support as an additional stretch goal.


## Team Members
- Jonathan Rubio: https://github.com/Osyki/