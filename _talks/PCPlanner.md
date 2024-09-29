---
title: "PC-Planner: Physics-Constrained Self-Supervised Learning for Robust Neural Motion Planning with Shape-Aware Distance Function"
collection: talks
type: "A research on the design of drive system for BLDCM and drive optimization"
permalink: /research_projects/1
venue: "State Key Laboratory of CAD&CG, Zhejiang University"
date: 2024-04-10
location: "Hangzhou, China"
---
*<font size=4>Advisor:</font> [<font size=4>Zhaopeng Cui</font>](https://zhpcui.github.io/)<font size=4>, Professor, College of Computer Science, Zhejiang University</font>*   

*April, 2024 - September, 2024.*  

- - -  

*Preview*  
==  

<p style="text-align: center; font-style: italic;">Overall Work</p>  

![PC_Planner](/images/PC_Planner.png)  

**Motion Planning (MP)** is a critical challenge in robotics, especially pertinent with the burgeoning interest in embodied artificial intelligence. Traditional MP methods often struggle with high-dimensional complexities. Recently, neural motion planners, particularly physics-informed neural planners based on the Eikonal equation, have been proposed to overcome the curse of dimensionality. However, these methods perform poorly in complex scenarios with shaped robots due to multiple solutions inherent in the Eikonal equation.

To address these issues, this work presents **PC-Planner**, a novel physics-constrained self-supervised learning framework for robot motion planning with various shapes in complex environments. To this end, we propose several physical constraints, including monotonic and optimal constraints, to stabilize the training process of the neural network with the Eikonal equation. Additionally, we introduce a novel **shape-aware distance field** that considers the robot's shape for efficient collision checking, addressing the computational intensity and facilitating adaptive motion planning at test time.

Experiments in diverse scenarios with different robots demonstrate the superiority of the proposed method in efficiency and robustness for robot motion planning, particularly in **complex environments**.

<p style="text-align: center; font-style: italic;">Preventing the converge to local minimum</p>  

![Local_min](/images/Local_min.png)

*Our Achievements*
==  

- We introduce a novel physics-constrained self-supervised learning approach for physics-informed neural robot motion planning, which enables efficient and robust motion planning for robots with various shapes in complex scenarios.
- We propose two physical constraints(PCs) to enable the network to jump out of local minima and converge to the correct solutions that obey the physical rules.
- We develop a new neural shape-aware distance field(SADF) for collision checking that can predict the minimum distance to the environment for any robot with arbitrary shapes and configurations in the fixed environment, which facilitates both self-supervised training and test stages.



*Physical Constraints*
==  
![PC_SADF](/images/PC_SADF.png)

2 inovations:  
- PC   --> minia --> complex shape
- SADF --> bvh --> prevent collision  
  
- - -  

*Results*
===  
- <p style = "text-align:justify; text-justify:inter-ideograph;"> Contributed to the development of a novel physics-constrained planner that learns the time fields and execute motion planning for robots of various shapes from any start state to any goal state in a self-supervised manner.</p>




