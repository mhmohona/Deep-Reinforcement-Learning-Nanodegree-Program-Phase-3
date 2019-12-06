### Learning Algorithm and implementation details:

In this project, a reinforcement learning agent is trained using **Deep Q-Learning with Experience Replay and Fixed Q-Targets** in a Unity Banana-Collector Environment to navigate a square world collecting yellow bananas and avoiding blue bananas.  

First, let's discuss the basic Q-Learning algorithm:  
#### Q-Learning:
The goal of Q-learning is to provide the agent with the capability of learning to act optimally in Markovian domains by experiencing the consequences of actions.

It finds a policy that maximizes the expected value of the total reward over any and all successive steps, starting from the current state.   

The algorithm has a function that calculates the quality of each state-action combination Q(s<sub>t</sub>,a<sub>t</sub>) 

![Img2](Assets/img2.png)

The shown Q-table is initialized with zeros. Then, at each time step t, the agent selects an action a<sub>t</sub>
, evaluates its consequences in terms of the immediate reward or penalty r<sub>t</sub> it receives, enters a new state s<sub>t+1</sub> (that depends on both the previous state s<sub>t</sub> and the selected action), and updates Q(s<sub>t</sub>,a<sub>t</sub>) as follows:

![Img1](Assets/img1.JPG)
By trying all actions in all states repeatedly, it learns which state-action pairs are best overall, judged by long-term discounted reward.
The Q-learning algorithm is shown below:   

![Img5](Assets/img5.PNG)
#### Deep Q-Learning:

In Deep Q-Learning The Q function is represented by a deep neural net instead of a table.
The network takes the current state as an input and outputs the q-value of each possible action associated with the current state q(s,a<sub>i</sub>). This gives the sense of the likelihood of each action being the best action to take.    
So, basicly, the input size of the net is the **state size(dimensionality)**  while its output size is the **number of possible actions** the agent can take.
![Img3](Assets/img3.PNG)

#### Experience Replay:
Experience replay lets online reinforcement learning agents remember and reuse experiences from the past. Here, a fixed length buffer is used to store a finite number of experiences tuples
<s<sub>t</sub>,a<sub>t</sub>,r<sub>t+1</sub>,s<sub>t+1</sub>>.   
A minibatch of these stored experiences is sampled and used to train the agent. The samples of the minibatch are drawn from a uniform distribution in order to break any temporal/chronological relationship between them.

 ![Img4](Assets/img4.png)

Experience Replay allows a more efficient use of previous experiences, by using them in the learning process over and over again. When gaining real-world experience is costly, then you can get full use of them.

#### Fixed Q-Targets:
Here, the Deep Q-Learning algorithm uses two separate newtworks with identical architectures: a primary Q-network and a target Q-network.
The target. The target Q-network parameters are updated less often than the primary Q-network. Without this, we would encounter a harmful form of correlation, where we shift the parameters of the network based on a constantly moving target.

Now, Here's the Deep Q-LEarning algorithm:

![Img6](Assets/img6.png)

#### About this project:
For this project, you will train an agent to navigate (and collect bananas!) in a large, square world.  

##### Reward:
A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana.  Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.  

##### Observation Space:
The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction. Given this information, the agent has to learn how to best select actions.  
##### Action Space: 
Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.
##### Goal:
The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.

##### Training Hyperparameters:
The agent is trained using the Deep Q-learning algorithm. The following Hyperparameters are used:   
1) Network Hyperparameters:   
```
Input Layer    : state dimensionality: 37   
Hidden Layer 1 : 64 units with ReLU activation functions.   
Hidden Layer 2 : 64 units with ReLU activation functions.   
Output Layer   : number of possible actions: 4   
Loss Function  : Mean Squared Error   
Optimizer      : Adam
Learning Rate  : 5e-4
Minibatch Size : 64
```  

2) Deep Q-Learning Hyperparameters:
```
Epsilon-greedy policy:
- Epsilon start           : 1.0   
- Epsilon min value       : 0.01   
- Epsilon Decay           : 0.995   

Decay Parameter GAMMA     : 0.99

Soft-Update Parameter TAU : 1e-3

Replay Buffer Size        : 1e5
```

#### Final Results:

Using Deep Q-Learning, the agent could solve the environment and collect more than 13 yellow bananas in less than 400 episodes.
![Img7](Assets/img7.png)
#### Ideas for future improvements:
1) Further hyperparameter tuning.
2) Using Double DQN
3) Using Prioterized Experience Replay
4) Using Dueling DQN




