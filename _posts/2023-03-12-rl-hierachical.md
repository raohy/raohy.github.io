---
layout: post
title: reinforce_hierachical_method
date: 2023-03-12
---

### A Deep Hierarchical Approach to Lifelong Learning in Minecraft  
when encoutering lifelong problem, efficient retention and tranfer prior knowledge to the new task is necessary because of the curse of diemension. The process is divided into 3 stage:  
1.retain previous knowledge   
2.needs the ability to choose relevant prior knowledge for solving new tasks.  
3.Ensures the effective and efficient interaction of the retention and transfer elements.  



### Policy distillation

temperature_softmax  
normal softmax: $\frac{e^(a_i)}{\sum_i e^(a_i)}$
temperature_softmax: 
eg.
softmax result:
[0.09003057317038046, 0.24472847105479767, 0.6652409557748219]
when t = 2，equals [1/2,2/2,3/2],calculate softmax, get：
[0.1863237232258476, 0.30719588571849843, 0.506480391055654]
when t = 0.5，equals [1/0.5,2/0.5,3/0.5],calculate softmax, get：
[0.015876239976466765, 0.11731042782619835, 0.8668133321973348]

so it is obvious that when t is larger the result getting more smooth, get more chance to explore the low probability choices.

so methods:
\tau = $\frac{\tau_0}{1+\log_{2}^{T}}$
T is the training times
so when the training progress, \tau decreases, making  the network become less smooth.

option is like a intra-policy that works under the whole process 


### The Option-Critic Architecture
The majority of the existing work has focused on finding subgoals and subsequently learning policies to achieve them. This method presents an alternative view, which blurs the line between the problem of discovering options from that of learning options(subgoals). We derive policy gradient theorems for options and propose a new option-critic architecture capable of learning both the internal policies and the termination conditions of options, in tandem with the policy over options, and without the need to provide any additional rewards or subgoals. 

option w