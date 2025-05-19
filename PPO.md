Overall goal is the same as any other policy gradient RL algorithm, teaches an agent how to act in an environment to maximize the overall reward. Where an agent acting is taking action like controlling a robotic hand. But PPO improves upon regular methods by making smaller more stable updates the the policy.

PPO restricts policy updates to stay close the old policy using "clipped surrogate objective" which penalizes large updates. This means that PPO's objective function has a clipped term in it. 

PPO collects "rollouts" a sequence of states, actions -> rewards and then updates both policy network (to act better) and value network (to estimate future rewards more accurately). The two networks interact
#### Objective Function: $LCLIP(θ)=Et​[min(rt​(θ)A^t​,clip(rt​(θ),1−ϵ,1+ϵ)A^t​)]$
Where $rt(θ)$ is the ratio of policies, $A^t$ is the "advantage estimate", how much better an action is than average, and ϵ is how much the policy can change from the previous one. 

This is made of 2 networks under the hood:
Actor - Policy Network (π):
- Outputs a probability distribution over actions
- used to calculate rt, adds entropy, samples action during training
Critic - Value Network (V):
- Outputs an estimate of future rewards from current state
- Calculates advantage, loss?

Training Loop:
- Collect N steps of interactions with the environment using the current policy
- Compute Loss and all related values
- Do some gradient descent something on minibatches?
- Update policy

PPO Hyper Parameters: 
- n_steps: how many steps to collect per rollout (2048)
- gamma: discount factor for future rewards when bootstrapping (0.99 higher cares about long term)
- gae_lambda: for advantage estimation (0.95)
- clip_range: max deviation from old policy  (0.2) -> increasing could make it harder to converge and more random
- desired_kl: not used in the loss function, just during training if it his too high or too low you can adjust the learning rate accordingly 
- entropy_coef: Used in the loss function with a log, entropy of one is log(1) which is 0%, encourages exploration 
- learning_rate: how fast the policy is updated
- batch_size, n_epochs: how much and how often to train per rollout
- lam: idk
- max_grad_norm: 
- value_loss_coef: used in the loss function for value network









Questions:
- How do policy updates work?
- what is the advantage estimate really?