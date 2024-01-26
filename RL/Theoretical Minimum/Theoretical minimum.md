 **RL problem statement (environment, agent, etc. abstraсtions). Markov decision process and its properties. Reward, discounted reward.
 
**Reinforcement Learning Problem Statement:**

1. **Environment (E):**
   - The external system with which the agent interacts.
   - It is characterized by a set of states, actions, transition dynamics, and a reward function.

2. **Agent (A):**
   - The entity that interacts with the environment.
   - Takes actions based on its current state to influence the environment.
   - Goal is to learn a policy or value function to maximize cumulative rewards.

3. **State (S):**
   - Represents the current situation or configuration of the environment.
   - Contains all relevant information for decision-making.
   - The state space is the set of all possible states.

4. **Action (A):**
   - Decisions or moves that the agent can take in a given state.
   - The action space is a set of all possible actions.

5. **Reward (R):**
   - A numerical signal provided by the environment after an action is taken in a certain state.
   - The agent's objective is to maximize the cumulative reward over time.

6. **Policy (π):**
   - The strategy or mapping from states to actions that the agent learns.
   - Defines the agent's behavior in the environment.

7. **Value Function (V or Q):**
   - Estimates the expected cumulative reward for a given state (V) or state-action pair (Q).
   - Helps evaluate the desirability of different states or actions.

**1) Markov Decision Process (MDP) and its Properties:**

![[Pasted image 20240120225520.png]]

A Markov Decision Process is a mathematical framework that formalises the RL problem. It consists of:

1. **State Space (S):**
   - A set of all possible states that the environment can be in.
   - The Markov property states that the future state depends only on the current state and action.

2. **Action Space (A):**
   - A set of all possible actions that the agent can take.

3. **Transition Probability Function (P):** функция перехода
   - Defines the probability of transitioning from one state to another given a specific action.
   $$ P(s', a, s) = \text{Pr}(S_{t+1} = s' | S_t = s, A_t = a) $$

4. **Reward Function (R):**
   - Defines the immediate reward received after taking a certain action in a certain state.
   - $R(s, a, s')$  is the reward obtained after transitioning from state \( s \) to \( s' \) by taking action \( a \).

5. **Policy (π):**
   - A strategy that the agent follows to select actions in different states.
   - Policies can be deterministic or stochastic.

**Discounted Reward:**

In many RL formulations, the concept of discounted rewards is introduced. The discounted sum of rewards, often denoted by $G_t$, is defined as:

$$ G_t = R_{t+1} + \gamma \cdot R_{t+2} + \gamma^2 \cdot R_{t+3} + \ldots = \sum_{k=0}^{\infty} \gamma^k \cdot R_{t+k+1} $$

Here, $\gamma$ is the discount factor (0 ≤ $\gamma$ < 1). It reflects the agent's preference for immediate rewards over delayed rewards. Introducing discounting ensures that the sum of rewards converges and the agent prioritises short-term gains while still considering long-term consequences.

![[Pasted image 20240121110901.png]]

Очень важное свойство, которое понадобиться в дальнейшем:

![[Pasted image 20240121111658.png]]


 **3) What is a Q-function and a Value-function? Relationship between them.  **

In reinforcement learning (RL), the Q-function (also known as the action-value function) and the value function are essential concepts used to estimate the expected cumulative rewards associated with taking certain actions in a given state. The relationship between these two functions lies in how they quantify the desirability of states and state-action pairs.

1. **Value Function (V-function):**
   - The value function, denoted as $V(s)$, estimates the expected cumulative reward starting from a particular state $s$ and following a certain policy $\pi$.
   - Mathematically, $V(s)$ is defined as the expected sum of discounted future rewards:
$$ V(s) = \mathbb{E}_\pi \left[ \sum_{t=0}^\infty \gamma^t R_{t+1} \mid S_0 = s \right] $$
   - It represents the long-term desirability of being in a particular state under a given policy.

2. **Q-function (Action-Value Function):**
   - The Q-function, denoted as $Q(s, a)$, estimates the expected cumulative reward starting from a state $s$, taking action $a$, and then following a certain policy $\pi$.
   - Mathematically, $Q(s, a)$ is defined as the expected sum of discounted future rewards:
     $$ Q(s, a) = \mathbb{E}_\pi \left[ \sum_{t=0}^\infty \gamma^t R_{t+1} \mid S_0 = s, A_0 = a \right] $$
   - It represents the long-term desirability of taking a specific action in a given state under a given policy.

**Relationship between Q-function and V-Function:**

The relationship between the Q-function and the V-function is expressed by the following equation, known as the Bellman Expectation Equation:

$V^{\pi}(s) = \sum_a \pi(a|s) Q^{\pi}(s, a)$

This equation states that the state-value function $V^{\pi}(s)$ is the weighted sum of the action-values $Q^{\pi}(s, a)$, where the weights are given by the probability of taking each action under policy $\pi$. In other words, the expected cumulative reward from a state $s$ under policy $\pi$ is the sum of the expected cumulative rewards of all possible actions, each weighted by the probability of selecting that action.

The formula expressing the Q-function in terms of the V-function and immediate reward is:

$$Q^{\pi}(s, a) = \sum_{s'} P(s_1 = s' \ | \ s, a) \cdot \left[ R(s, a) + \gamma \cdot V^{\pi}(s') \right] \cdot \pi(a|s)$$

=====

<b>How can RL be applied to NLP or CV tasks?  </b>

смотри отдельную страничку

NLP works well when
- good data
- diff loss function
- optimal model
when these requirements are not met, we may use RL and train on reward function.

===================

**What is an exploration to exploitation trade off?**

The exploration-exploitation trade-off is a fundamental concept in reinforcement learning and decision-making. It refers to the challenge of balancing the exploration of new possibilities with the exploitation of current knowledge to maximize rewards. In other words, it involves making decisions that not only leverage the information already acquired but also actively seek new information.

### Exploration:
- **Definition:** Exploration involves taking actions that are not currently believed to be optimal in order to gather more information about the environment.
- **Goal:** Discovering new states, uncovering the true values of actions, and refining the agent's understanding of the environment.

### Exploitation:
- **Definition:** Exploitation involves taking actions that are currently believed to be optimal based on the available knowledge.
- **Goal:** Maximizing short-term rewards by choosing actions that are expected to yield the highest immediate payoff.

### Trade-Off:
- **Challenge:** The trade-off arises because, to maximize cumulative rewards over time, an agent needs to exploit its current knowledge (choose actions it believes are optimal) while also exploring new options to refine that knowledge.
- **Dilemma:** Too much exploitation may lead to suboptimal long-term outcomes if the agent misses better actions. Too much exploration may result in inefficient decision-making in the short term.

### Strategies for Balancing Exploration and Exploitation:

1. **Epsilon-Greedy Strategy:**
   - With probability \(\epsilon\), choose a random action (exploration).
   - With probability \(1-\epsilon\), choose the current best-known action (exploitation).

2. **Softmax (Boltzmann) Exploration:**
   - Select actions probabilistically based on their estimated values.
   - Higher-value actions are more likely to be chosen, but all actions have a chance.

3. **UCB (Upper Confidence Bound) Exploration:**
   - Choose actions that have a balance between estimated value and uncertainty.
   - Prioritize actions that have a high estimated value and high uncertainty.

4. **Thompson Sampling:**
   - Sample actions from a distribution that represents the uncertainty about their values.
   - The uncertainty is updated based on observed outcomes.

5. **Exploration Decay:**
   - Gradually reduce the exploration rate over time as the agent gains more experience.

### Example Scenario:
Consider a scenario where an agent is learning to play a game. Initially, it may explore various actions to understand their effects (exploration). As it accumulates more experience and identifies actions that lead to higher rewards, it starts exploiting the known high-reward actions to maximize its immediate scores.

The challenge lies in finding the right balance. Too much exploration may result in missed opportunities for immediate reward, while too much exploitation may prevent the discovery of potentially better strategies in the long run. Effective reinforcement learning algorithms carefully manage this trade-off to achieve optimal performance over time.

===============

**5. Value-based vs. Policy based methods (general idea)**

Value-based and policy-based methods are two broad categories of reinforcement learning algorithms that approach the problem of learning optimal decision-making strategies in different ways. Here's a general idea of the key characteristics and differences between these two types of methods:

### Value-Based Methods:

1. **Objective:**
   - **Goal:** Learn the optimal value function, which assigns a value to each state or state-action pair.
   - **Decision-Making:** Make decisions by selecting actions that maximize the expected cumulative reward.

2. **Representation:**
   - **Value Function:** Represent the problem in terms of a value function, either the state-value function \(V(s)\) or the action-value function \(Q(s, a)\).
   - **Optimization:** Optimize the value function to find the most rewarding actions or policies.

3. **Examples:**
   - Q-Learning, Deep Q-Networks (DQN), Double Q-Learning, SARSA, etc.

### Policy-Based Methods:

1. **Objective:**
   - **Goal:** Directly learn the optimal policy, which defines the mapping from states to actions.
   - **Decision-Making:** Make decisions by sampling actions from the learned policy.

2. **Representation:**
   - **Policy:** Represent the problem in terms of a policy, often denoted as \(\pi(a|s)\), specifying the probability of taking each action given the current state.
   - **Optimization:** Optimize the policy to find the most rewarding actions or policies.

3. **Examples:**
   - REINFORCE, Actor-Critic, Proximal Policy Optimization (PPO), Trust Region Policy Optimization (TRPO), etc.

### Comparison:

- **Value-Based:**
  - **Advantages:** Often more sample-efficient in learning the optimal value function.
  - **Challenges:** May face difficulties in handling high-dimensional or continuous action spaces.

- **Policy-Based:**
  - **Advantages:** More naturally suited for continuous action spaces and can learn stochastic policies.
  - **Challenges:** Typically requires more samples to converge, especially in high-dimensional state spaces.

- **Hybrid Approaches:**
  - Some algorithms, like Actor-Critic, combine elements of both value-based and policy-based methods, benefiting from the strengths of each approach.

- **Trade-Off:**
  - The choice between value-based and policy-based methods often depends on the nature of the problem, the characteristics of the environment, and computational considerations.

In practice, the choice between value-based and policy-based methods depends on the specific requirements and constraints of the problem at hand. Hybrid approaches and more recent algorithms often aim to combine the benefits of both approaches.

===============

**6. What is the difference between model-based and model-free RL?**

В model-based мы вкурсе, о всех состояниях и знаем, с какой вероятностью мы перейдем в то или иное состояние, если совершим действие. А в model-free случае все сложнее, там мы этого не знаем.\

![[Pasted image 20240121223309.png]]