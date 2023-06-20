---
layout: post
title: lifelong problem
date: 2023-03-28
---


### A Lifelong Learning Approach toMobile Robot Navigation
Motivation:
Mobile robots often encounter new environments, and classic methods require experts to tune parameters based on experience or intuition. Current learning-based models, such as Deep Reinforcement Learning (DRL), suffer from bad generalization and tend to forget past parameters when training in a new environment. To solve this "lifelong learning" problem, three categories of approaches have been proposed: 1) regularization to prevent learned weights from deviating too much from old weights; 2) training generative models to recover old data for joint optimization; and 3) adopting dynamic network architectures for learning more tasks.

Intuition:
Catastrophic forgetting occurs when old knowledge is overwritten by new learning, resulting in difficulty navigating in specific scenarios. Therefore, the paper proposes a Lifelong Learning for Navigation (LLfN) framework that learns an auxiliary planner πθ to assist a classical planner π0 only in navigating difficult instances.

Comparison:
It's worth noting that LLfN has similarities to transfer learning, but it also considers backward transfer - how learning the current task can maintain or improve the performance of old tasks.

Method:
The paper uses Gradient Episodic Memory (GEM) from category one, which allows new experiences to improve performance on old tasks while imposing constraints on past jobs. 
![]({{site.url}}/assets/images/A_Lifelong_Learning_Approach_to/equation1.png)   
GEM optimizes the loss function with L(πθ,X) = E(s,a)∼X||πθ(s)−a||2.
![]({{site.url}}/assets/images/A_Lifelong_Learning_Approach_to/LLfm1.png) 

Training:
The paper proposes an approach for training mobile robots to navigate using a combination of classical planning and lifelong learning. The method is based on an initialized beginning policy, which can be random or based on a classical planner such as DWA, to explore the environment. The robot's experience is stored in a memory buffer, which is used to retain information about past experiences and improve performance on previous tasks.

To discriminate the performance of actions in a particular state, the paper proposes an algorithm based on heuristics extracted from DWA, which evaluates the quality of each action and selects the best one. If the performance is below a threshold, the best actions from the memory buffer are retrieved and used to update the buffer of the current environment. The policy is then optimized using GEM, which improves the robot's performance on past tasks while allowing it to learn new ones.

Prediction:
The proposed approach uses a combination of the beginning policy and the current policy to determine navigation. The beginning policy is used to explore the environment and collect experience, while the current policy is optimized using GEM to improve performance on past tasks and learn new ones. The resulting policy is then used to navigate the robot through the environment.

### LIFELONG ROBOTICRE INFORCEMENT LEARNING BY RETAINING EXPERIENCES
motivation: the standard multi-task reinforcement learning paradigm, which requires datacollection from each task in round-robin fashion, can often be unrealistic for embodied agents such as physical robots.
the main challenge is forward transfer. The traditional method is weight transfer which may discard important information from the past experiencesthat  are  relevant  to  future  tasks.
The author use the experience replay method. We measure the similarity between the past samples and the current task’s transition dynamics to determinewhich samples to transfer in the online fine-tuning phase.

related：
fine-tuning method: Efficient adaptation for end-to-end vision-based robotic manipulation. 2020
continual learning: Knowledge transfer in deep actor-critic reinforcement learning 2020
domain adapation: DARC 2021

### Towards Continual Reinforcement Learning:A Review and Perspectives
continual learning approaches:
1.explicit knowledge retention
1). parameter storage based
I.use of shared latent components
II.provide the representation of networks trained on previous task
    curse of dimension / storage requirement
    ->consider a single representation
III.store a prior about the extent of past usage of each parameters(popular)
context information
2).distillation based
3).rehearsal based
    experience replay
        improvement:learn to compress experiences during learning

2.leveraging shared structure
continual learning agents should reuse aspects of the solutions to previously solved subproblems through function composition by abstracting relevant meaningful information in the form of abstract concepts or skills.
1).modularity and composition focused
 Compositional generalization canbe understood as leveraging prior experience to solve compositional perturbations of priorproblems.
 decomposite the task into several modules, train in seperate modules and combine them together.
2).state abstractions focused
State abstraction (or aggregation) is central to the idea of capturing common structurewithin various tasks and potentially facilitating positive forward transfer across related tasks.
I. One such abstraction is state abstractions based on the PAC framework.
II. can be preserved while learning abstractionsis the underlying reward and transition model,
3).skill focused
4).goal focused
5).auxiliaary tasks focused

3.learning to learn
1).context detection
2).learning to adapt
the agent attempts to learn to alter its own optimization process based on historical success and failure.