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
   - The action space is the set of all possible actions.

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

3. **Transition Probability Function (P):**
   - Defines the probability of transitioning from one state to another given a specific action.
   $$ P(s', a, s) = \text{Pr}(S_{t+1} = s' | S_t = s, A_t = a) $$

4. **Reward Function (R):**
   - Defines the immediate reward received after taking a certain action in a certain state.
   - \( R(s, a, s') \) is the reward obtained after transitioning from state \( s \) to \( s' \) by taking action \( a \).

5. **Policy (π):**
   - A strategy that the agent follows to select actions in different states.
   - Policies can be deterministic or stochastic.

**Discounted Reward:**

In many RL formulations, the concept of discounted rewards is introduced. The discounted sum of rewards, often denoted by \( G_t \), is defined as:

$$ G_t = R_{t+1} + \gamma \cdot R_{t+2} + \gamma^2 \cdot R_{t+3} + \ldots = \sum_{k=0}^{\infty} \gamma^k \cdot R_{t+k+1} $$

Here, \( \gamma \) is the discount factor (0 ≤ \( \gamma \) < 1). It reflects the agent's preference for immediate rewards over delayed rewards. Introducing discounting ensures that the sum of rewards converges and the agent prioritises short-term gains while still considering long-term consequences.

![[Pasted image 20240121110901.png]]

Очень важное свойство, которое понадобиться в дальнейшем:

![[Pasted image 20240121111658.png]]


<b>What is a Q-function and a Value-function? Relationship between them.  </b>

In reinforcement learning (RL), the Q-function (also known as the action-value function) and the value function are essential concepts used to estimate the expected cumulative rewards associated with taking certain actions in a given state. The relationship between these two functions lies in how they quantify the desirability of states and state-action pairs.

1. **Value Function (V-function):**
   - The value function, denoted as \(V(s)\), estimates the expected cumulative reward starting from a particular state \(s\) and following a certain policy \(\pi\).
   - Mathematically, \(V(s)\) is defined as the expected sum of discounted future rewards:
$$ V(s) = \mathbb{E}_\pi \left[ \sum_{t=0}^\infty \gamma^t R_{t+1} \mid S_0 = s \right] $$
   - It represents the long-term desirability of being in a particular state under a given policy.

2. **Q-function (Action-Value Function):**
   - The Q-function, denoted as \(Q(s, a)\), estimates the expected cumulative reward starting from a state \(s\), taking action \(a\), and then following a certain policy \(\pi\).
   - Mathematically, \(Q(s, a)\) is defined as the expected sum of discounted future rewards:
     $$ Q(s, a) = \mathbb{E}_\pi \left[ \sum_{t=0}^\infty \gamma^t R_{t+1} \mid S_0 = s, A_0 = a \right] $$
   - It represents the long-term desirability of taking a specific action in a given state under a given policy.

**Relationship between Q-function and Value Function:**

The relationship between the Q-function and the value function is expressed by the following equation:

$$ V(s) = \max_a Q(s, a) $$

In words, the value of being in a state (\(V(s)\)) is the maximum expected cumulative reward achievable by taking any action in that state (\(\max_a Q(s, a)\)). In other words, the value function for a state is the maximum Q-value over all possible actions.

Conversely, the Q-function can be expressed in terms of the value function and the advantage function (\(A(s, a) = Q(s, a) - V(s)\)):

$$ Q(s, a) = V(s) + A(s, a) $$

This relationship helps in understanding that the Q-function provides a more detailed breakdown of the value of taking each action in a given state, while the value function focuses on the overall desirability of being in that state. Both Q-functions and value functions are crucial in various reinforcement learning algorithms, such as Q-learning and policy gradient methods.


<b>How can RL be applied to NLP or CV tasks?  </b>

...

- What is an exploration-exploitation tradeoff?  
- What is the difference between model-based and model-free RL?  
- Value-based vs. Policy based methods (general idea) 