[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"

# Project 1: Navigation

## Introduction

For this project, you will train an agent to navigate (and collect bananas!) in a large, square world.  

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana.  Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.  

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction.  Given this information, the agent has to learn how to best select actions.  Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.

## Methods

### Deep Q-Network (DQN)

A **DQN**, or **Deep Q-Network**, approximates a state-value function in a Q-Learning framework with a neural network.

#### **Hyperparameters** <br>
`BUFFER_SIZE` = int(1e5) <br>
`BATCH_SIZE` = 64 <br>
`GAMMA` = 0.99 <br>
`TAU` = 1e-3 <br>
`LR` = 5e-4 <br>
`UPDATE_EVERY` = 4

#### **Results**
Though score kept fluctuating up and down during training, we can observe a steady growth of the latter. The final score is about 13.12 obtained after 515 episodes.

![DQN Performance](images/performance_dqn.png) <br>

### Double DQN (DDQN)

One issue with Deep Q-Networks is they can overestimate Q-values (see [Thrun & Schwartz, 1993](https://www.ri.cmu.edu/pub_files/pub1/thrun_sebastian_1993_1/thrun_sebastian_1993_1.pdf)). The accuracy of the Q-values depends on which actions have been tried and which states have been explored. If the agent hasn't gathered enough experiences, the Q-function will end up selecting the maximum value from a noisy set of reward estimates. Early in the learning process, this can cause the algorithm to propagate incidentally high rewards that were obtained by chance (exploding Q-values). This could also result in fluctuating Q-values later in the process

We can address this issue using Double Q-Learning, where one set of parameters `w` is used to select the best action, and another set of parameters `w'` is used to evaluate that action.  

#### **Hyperparameters** <br>
`BUFFER_SIZE` = int(1e5) <br>
`BATCH_SIZE` = 64 <br>
`GAMMA` = 0.99 <br>
`TAU` = 1e-3 <br>
`LR` = 5e-4 <br>
`UPDATE_EVERY` = 4

#### **Results**
Though score kept fluctuating up and down during training, we can observe a steady growth of the latter. The final score is about 13.05 obtained after 478 episodes.

![DQN Performance](images/performance_ddqn.png) <br>


# In Future Works

## Prioritized Experience Replay (PER)

Experience replay lets online reinforcement learning agents remember and reuse experiences from the past. In prior work, experience transitions were uniformly sampled from a replay memory. However, this approach simply replays transitions at the same frequency that they were originally experienced, regardless of their significance. To replay important transitions more frequently, and therefore learn more efficiently, we use prioritized Experience Replay

## Dueling Agents (DA)

Dueling networks utilize two streams: one that estimates the state value function `V(s)`, and another that estimates the advantage for each action `A(s,a)`. These two values are then combined to obtain the desired Q-values.

## Rainbow
We can utilize the Rainbow Method `(DDQN + PER + DA)` which already led the ***Google Deepmind*** team to successfully train a complex agent efficiently and rapidly.

# Getting Started

1. Download the environment from one of the links below.  You need only select the environment that matches your operating system:
    - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
    - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
    - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
    - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)
    
    (_For Windows users_) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

    (_For AWS_) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux_NoVis.zip) to obtain the environment.

2. Place the file in the course GitHub repository, in the `p1_navigation/` folder, and unzip (or decompress) the file. 

3. Follow instructions in `Navigation.ipynb`.