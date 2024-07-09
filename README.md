# Reinforcement Learning Project - Omok

## Project Description

This project focuses on developing a reinforcement learning model to play the game of Omoku. The project was conducted using Google Colab.

## Problem Definition

- **State**: The state is represented by a 15x15 board for the game of Omoku.
- **Reward**: 
  - Win: +1
  - Lose: -1
  - Draw: 0
  - Placing 2 consecutive stones: 0.01 (A3C), 0.1 (TD)
  - Placing 3 consecutive stones: 0.02 (A3C), 0.2 (TD)
  - Placing 4 consecutive stones: 0.04 (A3C), 0.4 (TD)
  - Blocking opponent's 2 consecutive stones: 0.01 (A3C), 0.1 (TD)
  - Blocking opponent's 3 consecutive stones: 0.02 (A3C), 0.2 (TD)
  - Blocking opponent's 4 consecutive stones: 0.04 (A3C), 0.4 (TD)

To win, a player must place five stones in a row. Unlike traditional Omoku, both players can place stones without turn restrictions.

## Applied Reinforcement Learning Algorithms

### Temporal Difference Learning (TD)

#### Q-Learning

Q-Learning is a model-free reinforcement learning algorithm that updates the Q-function to learn the optimal policy.

1. **Initialization**: Initialize the Q-function \( Q(s, a) \) for all state-action pairs to 0. Set the initial state \( s_0 \).
2. **Episode Loop**: Repeat until the next state is terminal.
3. **Action Selection**: Select an action \( a_t \) in state \( s_t \) using an epsilon-Greedy policy.
4. **Action Execution and Reward Observation**: Execute the action \( a_t \), observe the next state \( s_{t+1} \) and reward \( r_t \).
5. **Q-function Update**: Update the Q-function using the observed reward and the maximum value of the next state.
6. **State Transition**: Transition to the next state \( s_{t+1} \).
7. **Termination Check**: If \( s_{t+1} \) is terminal, end the episode.

### Asynchronous Advantage Actor-Critic (A3C)

A3C improves learning speed by parallelizing the learning process across multiple agents.

1. **Initialization**: Initialize the global neural network (Actor and Critic). Set up multiple parallel environments (Workers).
2. **Worker Initialization**: Each Worker initializes its local neural networks and sets the initial state \( s_0 \).
3. **Start of Episode**: Each Worker begins an episode in its environment.
4. **Action Selection**: The Actor network selects an action \( a_t \) probabilistically based on the current state \( s_t \).
5. **Action Execution and Reward Observation**: Execute action \( a_t \), observe next state \( s_{t+1} \) and reward \( r_t \).
6. **Local Network Update**: Calculate the advantage, policy loss, value loss, and overall loss. Update the local networks.
7. **Global Network Update**: Periodically, Workers update the global network's parameters.
8. **State Transition**: Transition to the next state \( s_{t+1} \).
9. **Episode Termination**: If a terminal state is reached, the episode ends.

## Results

### TD Algorithm Evaluation
- The trained model consistently won against a random player, indicating successful learning.
- The model's consistent wins suggest overfitting as it always won, regardless of the opponent’s strategy.
- The absence of draws implies the reward structure influenced both aggressive and defensive play styles.

### A3C Algorithm Evaluation
- Similar to the TD algorithm, the A3C-trained model consistently won against a random player.
- The model also showed signs of overfitting, with no draws observed in matches between two trained models.
- A3C demonstrated faster training speeds compared to TD, with significant time savings during training.

## Conclusion

- **TD Learning**: Effective but prone to overfitting due to the state-space size.
- **A3C**: Faster training and similar performance, yet still faced overfitting issues.

For more reliable evaluation, real play data should be utilized to assess the model.

## Google Colab Links
- [Colab Notebook 1](https://colab.research.google.com/drive/1QYWusFlFOrPhcsVHwdg5NYKHjhxTR4vH?usp=sharing)
- [Colab Notebook 2](https://colab.research.google.com/drive/1y_7tR2MoWPw3Ie-x3_y3-ZzRSysti9zB?usp=sharing)

---

This README file provides an overview of your project, explaining the problem, the applied algorithms, and the results obtained. You can copy this text into a README.md file and upload it to your GitHub repository.
