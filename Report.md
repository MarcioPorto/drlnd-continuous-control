# DRLND Project 2 Report (Continuous Control)

## Introduction

For this project, I decided to work on solving the version of the Reacher environment with 20 agents. I chose to implement the DDPG algorithm, based on a [previous implementation](https://github.com/MarcioPorto/deep-reinforcement-learning/tree/master/ddpg-pendulum) for the `Pendulum` Gym environment. The decision to use DDPG was based on the fact that it extends the power of the popular DQN algorithm to environments with continuous action spaces, such as this. However, there are many other policy-based algorithms that might work well for solving this kind of environment, including: TRPO, PPO, and A3C.

## Learning Algorithm
## Plot of Rewards
## Future Work Ideas

If I had more time to work on this algorithm, I would look at the performance of other algorithms that have shown good results in environments with continuous action spaces. These include: 

I would also like to look for a better hyperparameter configuration that performs well with smaller episodes.

Other algorithms...

==================

## Algorithm and Implementation

The first step in the implementation of the algorithm involved starting out from the DDPG algorithm implemented in the Pendulum and Bipedal environments. I decided to keep the model definition the same since it very closely matched the model described in the original DDPG paper. As for the `DDPGAgent` class, there were a few changes based on the requirements of this project:

- The `act()` method was refactored to allow for picking actions for multiple agents before training the model. Running the method separately for each agent the way it was implemented in the Pendulum environment caused instability in the weights of the model as they were being updated very frequently.

During implementation, one 

As for the hyperparameters, I first tried to closely follow the ones mentioned in the original DDPG paper. However, I found that the agent was not training as fast as I had hoped. After some exploration, I realized that the L2 `WEIGHT_DECAY` param was causing the slowdown. The original paper used a value of `1e-2`, but I found that the algorithm trains faster and reliably with a weight decay of 0.
Was able to keep the same params as the Pendulum implementation.
Also tried to use other combinations of hyperparameters, including the original

As for `max_t` (the maximum number of time steps per episode), I started out with a value of 300, but found that the agent trains better with a larger value, such as 1000. I believe this is the case because the agent gets to learn how to follow the target better because it is forced to do so for a longer period of time.

## Notes

- Using Gaussian distribution instead of random in OU Noise seems to help a lot
- Changes from original:
    - Number of nodes in network