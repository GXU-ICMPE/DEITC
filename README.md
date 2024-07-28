# Demonstration-Environment-Infromed Task Chaining for SC-AIRL of Long-Horizon Tasks
Guangyu Xiang, Shaodong Li*, Guangxi University, Nanning, China (Code is coming soon)
# Introduction
In this work, we were interested in investigating the efficacy of SC-AIRL on long-horizon tasks. SC-AIRL is a form of Inverse Reinforcement Learning (IRL) that decomposes long-horizon tasks into multiple sub-tasks, where a discriminator, acting as a reward signal, and sub-policies are simultaneously learned using expert data. Empirically, we found that this state-of-the-art IRL-based method is unable to effectively solve longer-horizon manipulation tasks. We demonstrated that this is because SC-AIRL is susceptible to state shifts, where starting the next sub-task from an unsuitable state can lead to failure. Below, we show the connection process of SC-AIRL and a simplified example where this occurs：
![Figure_1](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/Figure_1.png)
# Method
To address the limitations of SC-AIRL in long-horizon tasks, we propose Demonstration-Environment-Informed Task Chaining. Specifically, while training the sub-policies, we simultaneously train a chaining policy using expert data to fine-tune the sub-policies. Additionally, we use environment feedback to help the chaining policy learn to end the current sub-task in an appropriate terminal state. Our method's process is as follows:
![image](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/Figure_3.jpg)
where the chaining policy takes the current state and sub-task index as inputs to evaluate whether the current state is suitable as a terminal state. The chaining policy is trained using reinforcement learning (RL), with rewards coming from both expert demonstrations and environment feedback. The chaining policy is considered as a function, denoted as CP, and its output is used as an auxiliary reward signal to fine-tune the sub-policies.
# Experiments Setup
We test our method in three long-horizon tasks with main baselines(SC-AIRL/T-STAR):
![image](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/Figure_4.jpg)
# Experimental videos:
T-STAR\SC-AIRL\DEITC in Stack task: <br>
![T-STAR in Stack task](https://github.com/Guangyu-Xiang/DEITC/blob/main/STACK/Stack-TSTAR.gif) ![SC-AIRL in Stack task](https://github.com/Guangyu-Xiang/DEITC/blob/main/STACK/Stack-SC.gif) 
![DEITC in Stack task](https://github.com/Guangyu-Xiang/DEITC/blob/main/STACK/Stack-DEITC.gif) <br>
T-STAR\SC-AIRL\DEITC in Stack Three task: <br>
![T-STAR in Stack Three task](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/TSTAR.gif) ![SC-AIRL in Stack Three task](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/SC.gif) 
![DEITC in Stack Three task](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/deitc.gif) <br>
T-STAR\SC-AIRL\DEITC in Insert Two task: <br>
![T-STAR in Insert Two task](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/Tstar.gif) ![SC-AIRL in Insert Two task](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/SC.gif) 
![DEITC in Insert Two task](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/DEITC.gif) <br>
# Ablation Study:
In this section, we further explore the impact of design variations in DEITC: 1) ablation study on the rewards for the chaining policy; 2) ablation study on fine-tuning the sub-policies and the automatic selection of terminal states.<br>
DEITC-Demon: Chaining policy is only train through Demonstrations <br>
![GIF](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/demon.gif) <br>
DEITC-Env: Chaining policy is only train through Envrionment feedback <br>
![GIF](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/env.gif) <br>
DEITC-oAuto: Subpolicy is only train with automatically terminate subtask but without fine-tuning <br>
![GIF](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/oAUTO.gif) <br>
DEITC-nAuto: Subpolicy is only train with fine-tuning but without selecting terminal states <br>
![GIF](https://github.com/Guangyu-Xiang/DEITC/blob/main/Three/nAUTO.gif) <br>
# Empirical analysis:
Three-dimensional coordinates of the positions where the robot end-effector grasps the red block (i.e. terminal states) in the Stack Three task. <br> 
Left: The policy learned by DEITC selects terminal states for completing the current subtask that show a higher degree of overlap with the terminal states in expert demonstrations. <br> 
Right: In SC-AIRL, using the Goal set to select the terminal states leads to significant deviation from expert demonstrations, potentially causing failure in subtask connections. <br>
![image](https://github.com/Guangyu-Xiang/DEITC/blob/main/INSERT/Figure_5.jpg) <br>

