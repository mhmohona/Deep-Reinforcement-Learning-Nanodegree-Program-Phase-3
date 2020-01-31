# Project Three: Collaboration and Competition

**Q1:** I had a very weird experience with training, when I train with GPU enabled, the agent doesn't improve over more than 2000 episodes. When I disabled GPU, the environment was solved in about 1200 episodes! What could be the cause of that?!

*MSJose:* I think I read somewhere (in a lesson?) that in RL/DRL some problems are better solved without a GPU. @Reham El-Kholy Which algo are you trying for P3? @andreiliphd used PPO successfully; I stuck with MADDPG! (The acronym just "feels" very powerful :sunglasses:

---

**Q2:** I just examined the code in MADDPG Lab. I guess I need to alter the main.py and maddpg.py for a working solution. So changing the environment and decreasing the number of agents to two? Seems a bit difficult, as the 3dot environment is a bit mixed in the code in the main.py. Ok, tomorrow I will try. Any tip to prevent me banging my head into the wall some times?

*MSJose:*
I'm curious to know how that goes with you... the tensorboard shell script didn't work for me so I didn't  spend much time on that lab. I followed the recommendation in 5. Benchmark Implementation; i.e., I based my project solution on the provided P3 L05. ddpg-bipedal code. I found it easier to convert to multi-agent than use the MADDPG implementation in the lab. BUT use whatever you feel like working on. 
Good luck :shamrock:

---

**Q3:** I haven't tried yet but since the reward is sparse and at first the moves are random, there is no much reward to make our agents learn. Prioritized Experience Replay should help the agent converge faster. Have anyone tried?

*Ruben Chaves:*
It seems like it won't work if your training is unstable. The priority depends on the TD error and if your model is not working well, you'll have big errors(I'm talking errors in the millions), giving priority to unstable samples (big gradients that have to be clipped). Maybe I'll try later if I get a more stable training loop (I haven't solved the environment yet).
:heavy_check_mark:

*Ellyana Linden:*
You can try different learning rates for actor and critic. I set actor 2e-4 and critic 3e-4; and second trial 2e-4 and 5e-4, both reached score of 0.5 around 1014 and 1042 respectively. Increase the Tau value, maybe you'll get a better result. I got 0.5 in 840 episodes using simple DDPG single Actor and Critic :grin:

---


**Q4:** Firstly, Random Seed: I have been looking at how random seed is used and get conflicting views about whether to just set it once globally or to pass seed into every consumer and reset random seed locally. The Pytorch forum especially seems to favour the global approach, or at least I should say almost every example of using random seed goes something like this, which implies set once and forget:
```python
SEED = 1
random.seed(SEED)
np.random.seed(SEED)
torch.manual_seed(SEED)
if torch.cuda.is_available(): torch.cuda.manual_seed_all(SEED)
```
Anyone have an opinion about this - set it once or pass seed into every consumer / class?

Secondly, I have a couple of examples of the OUNoise class that use different random number generation approaches when setting dx:
`dx = self.theta * (self.mu - x) + self.sigma * np.array([random.random() for i in range(len(x))])`
and
`dx = self.theta * (self.mu - x) + self.sigma * np.random.standard_normal(self.size)`
An experiment on using these shows that the np.array over the random.random produces only positive values in the range of 0 to (almost) 1, whereas the np.random.standard_normal produces a range around zero that can go under -1 and over 1. Is one better than the other for this purpose?
```python
x = [0,1,2,3,4,5,6,7,8,9]
size = len(x)
print(np.array([random.random() for i in range(size)]))
print(np.random.standard_normal(size))
```
```markdown
[0.58758061 0.882479   0.84619742 0.50528382 0.58900226 0.03452583
 0.24273997 0.79740425 0.414314   0.1730074 ]
[-0.69166075 -0.39675353 -0.6871727  -0.84520564 -0.67124613 -0.0126646
 -1.11731035  0.2344157   1.65980218  0.74204416]
```

*MSJose:*
"Seed" - at least in ML - is the initialization of a pseudo-random number generator. Its main use is reproducibility. I have done many courses and specializations in Python and R, at Coursera, edX, IBM, Google, Amazon, Facebook, Codecademy, DataCamp, and Udemy, and all of them use the set once globally approach.

*Chris Palmer:*
:+1: Thanks @MSJose! Do you have any opinion regarding the setting of dx in the second part of the question?

*MSJose:*
@Chris Palmer The following works well for me, so I don't normally change things for the sake of changing things.
`dx = self.theta (self.mu - x) + self.sigma np.array([random.random() for i in range(len(x))])`
Cheers!




---

---

---

## Tips from MSJose

**Rubric Requirements:**

In order to solve the environment, your agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents).
Here's my final result:

![image](https://user-images.githubusercontent.com/14244685/73573068-a14d3500-449c-11ea-8fa9-8f6fe786b9d0.png)

**(Optional) Challenge: Play Soccer**

The Unity Soccer Twos environment consists of four agents competing in a 2 vs 2 toy soccer game. There is a goalie and a striker for each team. The Striker tries to get the ball into the opponent's goal, while the Goalie tries to prevent the ball from entering its own goal. One team is being trained while the other is taking random actions.
If a goal is scored, the scoring team gets 1.1 points; otherwise, zero points for each team. Over 100 games, the maximum possible score for a team is 110 (1.1 x 100).
The environment is considered solved when the trained team scores a goal in and wins 100 consecutive games. (You would think a team taking random actions in soccer is easy to beat; in reality it is not.)

Finally, after several days and nights, SUCCESS - in 12,704 episodes x 600 steps!

![image](https://user-images.githubusercontent.com/14244685/73573121-c772d500-449c-11ea-8769-52bb1bf088fb.png)

When you complete p3, it would be good if you can publish your result, together with the algo and training time. PPO and MADDPG have been used successfully on p3. Everyone is of course strongly encouraged to try different algorithms (given enough time) and see which ones work best. That's how we learn better at AI - by experimenting. Just look at how DRL is now being used for Computer Vision problems :grinning:

**[MADDPG vs PPO]**
If you are doing, or about to do, p3: here are some (unscientific) stats I observed.
I ran my MADDPG solution 50 times, and did the same with the PPO solution I was working on. The MADDPG solution converged 25 times out of 50 (=50%) within the 1200 episodes/iteration allotted, while the PPO solution converged only 4 times (=8%).
The range of convergence for MADDPG was 758 to 1049 episodes, with a mean of 912, while for PPO it was 959 to 1098, with a mean of 1032.
I purposely lowered num_episodes to 1200 to make it tougher for both algorithms to converge.
Anyway, take this with a grain of salt. Perhaps my PPO solution is really flawed, and you can come up with a lot better implementation of PPO for p3.
However, if you want a comparatively quicker way to do p3, use MADDPG. Of course, you are always encouraged to try other algorithms like PPO. That's how we increase our knowledge :grinning: Good luck :shamrock:
Here's the plot of MADDPG vs PPO (my implementations anyway).

![image](https://user-images.githubusercontent.com/14244685/73573354-5ed82800-449d-11ea-89dd-be1793afbc4e.png)


With a Little Help from My Friends (courtesy of The Beatles, 1967)
For the Survivors about to do p3, here's a (alternative to DDPG) starter code based on MADDPG to get you going over the last obstacle.
NOTES:
1. The two .py files are complete and working. You do not need to modify these, except if you want to tune one or two parameters.
2. The .ipynb file is almost complete. You just have to fill in part of the body of the maddpg() function, specifically the loop.
   *** In fairness to the roughly 60% of Survivors who have already graduated, I am not providing the complete code this time. ***
3. Remember that there are two agents in the MADDPG code. That means you have to address these two in your loop implementation.
4. With a correctly-written loop:
   a. You can expect to solve the environment in 600-800 episodes on average, well below the given n_episodes=1500 in the call to maddpg().
   b. You should expect the training to run between 5 to 15 minutes - quite fast compared to p2.  (With GPU enabled)
   c. The complete p3 code was run in the Workspace, so it is guaranteed to converge there; i.e., solve the environment in 1500 episodes or less.
   d. IF YOU GO OVER 1500 EPISODES OR 30 MINUTES WITHOUT CONVERGING, it most probably means your implementation is incorrect.
5. Take a quick look at this starter code and gauge whether you think it will speed up your completion of the p3 project.
6. IF you have started already on p3 and making progress regardless of the algorithm, stick with that.
7. Finally, good luck :shamrock: and see you all at the finish line!

---

## Tips from István  

Just thinking: there are interesting options for experiment with multiple agents.
Making the actor neural networks a bit different for all agents can result in strange behaviors. In cases of far more than two agents, it can even help to build better final models.
Idea: Initialize for all agents a bit different neural network, and train. After training select the best agents, or if two agents scores are very close select the simpler network. Then train again assigning this best network to all agents.
Maybe this is a bit overkill, as we can't even really cover the hyperparameter space, but can work. And if the size of the network matters we can even find some satisfying minimum network easier.


---

## Tips from Vova

Has anyone tried different randomization for agent's actions? I tried simple Gaussian noise and it worked much better than Ornstein-Uhlenbeck.
If you check how training runs in graphical non-training mode, you can see that Ornstein-Uhlenbeck noise seem to push paddles in almost same direction every episode.
Maybe it's so sensitive to seed because of that?
With gaussian I've tried several seeds and it doesn't affect too much, solving within ~400 episodes.
