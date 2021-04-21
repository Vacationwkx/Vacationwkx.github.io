---
title: "Reinforcement Learning Notes"
date: 2020-12-08T08:47:38+08:00
draft: false
tags:
  - reinforcement learning
---

## [State Representation](https://ai.stackexchange.com/questions/7763/how-to-define-states-in-reinforcement-learning)

- state vector ( obey Markov Property)
- observation →knowledge→ state
- [Partially observable Markov decision process](https://en.wikipedia.org/wiki/Partially_observable_Markov_decision_process)
- "learning or classification algorithms to "learn" those states"
    - A simple linear regression
    - A more complex non-linear function approximator, such as a multi-layer neural network.

The Atari DQN work by DeepMind team used a combination of feature engineering and relying on deep neural network to achieve its results. The feature engineering included downsampling the image, reducing it to grey-scale and - importantly for the Markov Property - using four consecutive frames to represent a single state, so that information about velocity of objects was present in the state representation. The DNN then processed the images into higher-level features that could be used to make predictions about state values.

## Policy Gradients

[Deep Deterministic Policy Gradient - Spinning Up documentation](https://spinningup.openai.com/en/latest/algorithms/ddpg.html)

[Mathe Funda](https://danieltakeshi.github.io/2017/03/28/going-deeper-into-reinforcement-learning-fundamentals-of-policy-gradients/)

## Deep Reinforcement Learning

### VDQN

![DQN](/rl/dqn.png)

DeepMind used atari environment for DQN test, even through all the return `observation` for preprocessing:

#### Preprocessing

- Observation
  1. rgb $\rightarrow$ gray, i.e. image shape (210,160,3)$\rightarrow$ (210,160)
  2. down sample: (210,160) $\rightarrow$ (110,84)
  3. crop: (110,84) $\rightarrow$ (84,84)
- Observation :arrow_right: state:
  1. 4 history frames to 1 $\rightarrow$ (84,84,4)

#### CNN

![CNN of DQN](/rl/atari_cnn.png)

- architecture
  - Conv2D: 32, 8x8, strides=4, input_shape=(84,84,4)
  - Conv2D: 64, 4x4, strides=2
  - Conv2D: 64, 3x3, strides=1
  - Dense: 256
  - Dens: outputshape

- comple
  - RMSProp

#### Replay Buffer

- fix length
- every time feed: (state, action, reward, next_state, done)
- once reach L length: start training
- length: 1million

#### Target model update

- every C step
- Epsilon: 1$\rightarrow$0.1 (1 million frame for total 50 milion)

#### Frame skipping

![Frame skip](/rl/frame_skip.png)

[great explanation](https://danieltakeshi.github.io/2016/11/25/frame-skipping-and-preprocessing-for-deep-q-networks-on-atari-2600-games/)

- chose at kth frame
- last k-1 frame
- k=4

Speed up for atari, use `info['ale.lives'] < 5` for terminating the episode

#### Clip

- reward: -1,0,1
- Error: $|Q(s,a,\theta)-Q(s',a',\theta^-)\le1$ 

NOTES:

change RMSprop parameter

```python
tf.keras.optimizers.RMSprop(
    learning_rate=0.00025,
    rho=0.9,
    momentum=0.95,
    epsilon=1e-07,
    centered=False,
    name="RMSprop",
    **kwargs
)
```

#### Random Gym Run

- Frame:10,000
- Reward: 4-2, 5-0

### [Double DQN](https://medium.com/analytics-vidhya/building-a-powerful-dqn-in-tensorflow-2-0-explanation-tutorial-d48ea8f3177a)

- main: choose action
- target: update Q in Bellman as Q_max
- model fit: fit the main with target value output
- after same iterations, copy main weights and biases to target

### [DuelingDQN](https://towardsdatascience.com/dueling-deep-q-networks-81ffab672751)

maybe drop DQN

![Perform on atari](/rl/drl_compare.png)

[source](https://www.toptal.com/machine-learning/deep-dive-into-reinforcement-learning)

- [x] DDQN Architecture
- [x] ~~custom model fit for weights~~ too complicated
- [x] Priorited Replay
  - [x] paper
  - [x] code
  - [x] test
- [x] Agent
- [x] Train Main

### DQN Parameter Adjustment

https://github.com/dennybritz/reinforcement-learning/issues/30

https://www.reddit.com/r/reinforcementlearning/comments/7kwcb5/need_help_how_to_debug_deep_rl_algorithms/

### A3C

- [x] David Sliver
- [x] [Policy Gradient Mathe](https://medium.com/@thechrisyoon/deriving-policy-gradients-and-implementing-reinforce-f887949bd63)
- [x] Paper review
- [ ] ~~Example threading Pytorch~~
- [ ] ~~Code for Pendulum~~

### A2C

[Why A2C not A3C](https://github.com/ikostrikov/pytorch-a3c)

- [Two head Network](https://www.datahubbs.com/two-headed-a2c-network-in-pytorch/)
- **Why Entropy**: https://awjuliani.medium.com/maximum-entropy-policies-in-reinforcement-learning-everyday-life-f5a1cc18d32d#:~:text=Because%20RL%20is%20all%20about,the%20actions%20an%20agent%20takes.&text=In%20RL%2C%20the%20goal%20is,term%20sum%20of%20discounted%20rewards
  - Entropy is great, but you might be wondering what that has to do with reinforcement learning and this A2C algorithm we discussed. The idea here is to use entropy to encourage further exploration of the model
  -  to prevent premature convergence
- Negative Loss:
  - TensorFlow and PyTorch currently don’t have the ability to maximize a function, we then minimize the negative of our loss
- [Accumulated gradient](https://discuss.pytorch.org/t/how-to-implement-accumulated-gradient/3822)

### PPO

- debug for sub optimal:

  - [possible solutions](https://www.reddit.com/r/reinforcementlearning/comments/d3wym2/catastrophic_unlearning_in_ppo_a_plausible_cause/)                    

    - decrease lr
    - decrease lambda during program               

  - It would be helpful to output more metrics, such as losses, norms of the gradients, KL divergence between your old and new policies after a number of PPO updates.[source](https://www.reddit.com/r/reinforcementlearning/comments/bqh01v/having_trouble_with_ppo_rewards_crashing/?utm_source=share&utm_medium=web2x)

  - change algo

    > It depends on the environment. Something like ball balancing might just tend to destabilize with PPO, vs. something like half cheetah that is less finicky balance wise. You might try using td3 or sac, but with ppo you might just have to early stop. There might be some perfect combo of lr and clip param that leaves it stabilized... maybe with using another optimizer as well like classic momentum or adagrad.
    >
    > [source](https://www.reddit.com/r/reinforcementlearning/comments/bqh01v/having_trouble_with_ppo_rewards_crashing/?utm_source=share&utm_medium=web2x)

  - 

## Material

#### Powerup Knowledge

- [How to Exploration](https://towardsdatascience.com/a-short-introduction-to-go-explore-c61c2ef201f0)
- [Why RL Hard](https://www.alexirpan.com/2018/02/14/rl-hard.html)
- [DRL Sucks](https://www.reddit.com/r/MachineLearning/comments/bdgxin/d_any_papers_that_criticize_deep_reinforcement/)

### Intro

[An Introduction to Deep Reinforcement Learning](https://thomassimonini.medium.com/an-introduction-to-deep-reinforcement-learning-17a565999c0c)

### DRL

#### Reward shaping

[reference](https://www.youtube.com/watch?v=0R3PnJEisqk&ab_channel=Bonsai)

#### Code for model

- [Tensorflow](https://github.com/marload/DeepRL-TensorFlow2)
- [Pytorch](https://github.com/bentrevett/pytorch-rl)
  - [Simple to create Model](https://github.com/FrancescoSaverioZuppichini/Pytorch-how-and-when-to-use-Module-Sequential-ModuleList-and-ModuleDict)
  - [PPO](https://github.com/ikostrikov/pytorch-a2c-ppo-acktr-gail)

#### Course

- [CS 285](http://rail.eecs.berkeley.edu/deeprlcourse/)

- [Deep Reinforcement Learning](http://videolectures.net/rldm2015_silver_reinforcement_learning/)

#### Blog

- [Atari](https://neuro.cs.ut.ee/demystifying-deep-reinforcement-learning/)
- [Medium](https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0)
- [Tensorflow Code](https://github.com/marload/DeepRL-TensorFlow2)
- [Start from PONG](https://towardsdatascience.com/tutorial-double-deep-q-learning-with-dueling-network-architectures-4c1b3fb7f756)
- [Nice Dude](https://danieltakeshi.github.io)

#### Atari

- [Monitor / Video using X11](https://hub.packtpub.com/openai-gym-environments-wrappers-and-monitors-tutorial/)
- [Recap](https://rubenfiszel.github.io/posts/rl4j/2016-08-24-Reinforcement-Learning-and-DQN.html)

#### CNN

- parameter calculation : https://medium.com/@iamvarman/how-to-calculate-the-number-of-parameters-in-the-cnn-5bd55364d7ca#:~:text=To%20calculate%20it%2C%20we%20have,3%E2%80%931))%20%3D%2048
- [output shape calculation](https://cs231n.github.io/convolutional-networks/#pool)

### API for Vrep

[Legacy remote API](https://www.coppeliarobotics.com/helpFiles/en/legacyRemoteApiOverview.htm)

[Remote API functions (Python)](https://www.coppeliarobotics.com/helpFiles/en/remoteApiFunctionsPython.htm)

### David Silver - 4/10

[Teaching - David Silver](https://www.davidsilver.uk/teaching/)

### The Book - Ch5

[Reinforcement Learning: An Introduction](http://incompleteideas.net/book/the-book.html)

[Code for it:](http://incompleteideas.net/book/code/code2nd.html)

[Reinforcement Learning: An Introduction](https://waxworksmath.com/Authors/N_Z/Sutton/RLAI_1st_Edition/sutton.html)

### Paper

[Keypaper](https://spinningup.openai.com/en/latest/spinningup/keypapers.html)

### Training Software

[Gym: A toolkit for developing and comparing reinforcement learning algorithms](https://gym.openai.com/)

### Open cv

- [resize](https://chadrick-kwag.net/cv2-resize-interpolation-methods/)