---
title: "Physics-Constrained Self-Supervised Learning for Robust Neural Motion Planning with Shape-Aware Distance Function (under revision)"
type:
collection: publications
permalink: 2024-paper-2
excerpt: 'Robot neural motion planning'
venue:
location:
paperurl:
---

*<font size=4>Advisors:</font> [<font size=4>Zhaopeng Cui</font>](https://zhpcui.github.io/)<font size=4>, State Key Laboratory of CAD&CG, College of Computer Science, Zhejiang University</font>*   


*Preview*  
==  

<p style="text-align: center; font-style: italic;">Overall Work</p>  

![PC_Planner](/images/PC_Planner.png)  

**Motion Planning (MP)** is a critical challenge in robotics, especially pertinent with the burgeoning interest in embodied artificial intelligence. Traditional MP methods often struggle with high-dimensional complexities. Recently, neural motion planners, particularly physics-informed neural planners based on the Eikonal equation, have been proposed to overcome the curse of dimensionality. However, these methods perform poorly in complex scenarios with shaped robots due to multiple solutions inherent in the Eikonal equation.

To address these issues, this work presents **PC-Planner**, a novel physics-constrained self-supervised learning framework for robot motion planning with various shapes in complex environments. To this end, we propose several physical constraints, including monotonic and optimal constraints, to stabilize the training process of the neural network with the Eikonal equation. Additionally, we introduce a novel **shape-aware distance field** that considers the robot's shape for efficient collision checking, addressing the computational intensity and facilitating adaptive motion planning at test time.

Experiments in diverse scenarios with different robots demonstrate the superiority of the proposed method in efficiency and robustness for robot motion planning, particularly in **complex environments**.

<p style="text-align: center; font-style: italic;">Preventing the converge to local minimum.</p>  

![Local_min](/images/Local_min.png)

*Our Achievements*
==  

- We introduce a novel physics-constrained self-supervised learning approach for physics-informed neural robot motion planning, which enables efficient and robust motion planning for robots with various shapes in complex scenarios.
- We propose two physical constraints to enable the network to jump out of local minima and converge to the correct solutions that obey the physical rules.
- We develop a new neural shape-aware distance field(SADF) for collision checking that can predict the minimum distance to the environment for any robot with arbitrary shapes and configurations in the fixed environment, which facilitates both self-supervised training and test stages.


<p style="text-align: center; font-style: italic;">The PC-Planner integrates a physics-constrained self-supervised learning framework with a shape-aware distance field.</p>  

![PC_SADF](/images/PC_SADF.png)  


*Experiments*
===  

<p style="text-align: center; font-style: italic;">Comparison of motion planning in 3D for grid robots. The optimal results are highlighted.</p>  


<img width="837" alt="Screenshot 2024-10-02 at 2 17 52 PM" src="https://github.com/user-attachments/assets/bb0f8b86-1690-4a44-807b-d75305176a73">

We analyze and validate our method with different robots and environments. We compare our methods(with and without adaptive planning) with the baselines NTFields [Ni and Qureshi 2023a], P-NTFields [Ni and Qureshi 2023b], FMM [Sethian 1996], RRT [Kingston et al. 2018], RRT-Connect [Kuffner and LaValle 2000], and LazyPRM [Bohlin and Kavraki 2000]. Our evaluation metrics include path length, planning time, success rate (SR) and challenging success rate(CSR).  
We perform a comparative analysis of our method against the baselines in two complex 3D Gibson environments (Arona and Eastville) [Xia et al. 2018] in SE(2) and SE(3) space with rigid robots. In those two Gibson environments, we employ different robots. In one scenario, we deploy a mobile robot, a bear, and a bird for navigation within the environment. In the other scenario, we showcase the use of a piano, a toy car, and a drone to plan in the environment. Specifically, the mobile robot, bear, piano, and toy car navigate in SE(2) space with 3 Degrees of Freedom (DoFs) while the bird and drone plan in SE(3) space with 6 DoFs. In the Arona environment, our proposed method demonstrates **the best SR, CSR, and path length** with competitive computation time. It is worth mentioning that without adaptive planning, our method achieves **minimal computation time** and **the best or second-best SR, CSR, and path length** in most tasks. Moreover, our method is more efficient compared to traditional methods, ranging from at least **40 times to as much as 200 times faster** than traditional methods, indicating an affordable time cost of our adaptive strategy. This highlights the effectiveness and superiority of our proposed method.
