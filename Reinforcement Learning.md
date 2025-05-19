
Value-Based VS Policy Gradient RL

| Concept               | Value Based Methods (Q-Learning, DQN)                              | Policy Gradient Methods (PPO, SAC)                             |
| --------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------- |
| What is being trained | A value function (Q-value: state-action -> reward model)           | A policy (a function that maps states to actions)              |
| Picking actions       | Pick the action with the highest q value (ε-greedy) = argmaxQ(s,a) | Sample / pick actions from the policy distribution = πθ​(a∣s)  |
| Action Space          | Usually discrete because of the nature of the value funciton       | Discrete or continues space                                    |
|                       |                                                                    |                                                                |
TDMPC2:
- Reverse of what we were doing before, rl trains world model using TD learning which is then used in MPC to take action 

PPO (proximal policy optimization): 
- Take steps based on the gradient but dont want to destroy the paramters

On Policy RL:
- Agent can pick actions
- Agent always follows policy

Off Policy RL:
- Agent doesnt pick actions
- learn from expert
- learn from buffer