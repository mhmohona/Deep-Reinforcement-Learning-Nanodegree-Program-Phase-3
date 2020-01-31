**Q1: I tried Udacity official implementation DPDG, it needs a significant tuning. What models are you trying?**

*z0k:* I haven’t attempted this one yet. Still working through the first part of the ND. It was this project https://github.com/udacity/RL-Quadcopter

*Andrei Li:* Udacity owns flying cars company. If a manual is like Udacity course I guess pilots will be professional mathematicians. Strange but I love that in Udacity.

---

**Q2:** I have been training single agent since yesterday. My average score seemed to be in the local minima, didn't want to improve. I tried various fc1, fc2, sigma, learning rate actor, lr critic, added normalization batch. Would you give me a hint what I should add/change? I follow the pendulum code from the lesson. Thanks. My results are attached. I have another 3 more like those results. 
![image](https://user-images.githubusercontent.com/14244685/73553283-df822e80-4473-11ea-91ba-c2014244dbf5.png)

*MSJose:* It's good you are basing your **p2** on **ddpg-pendulum**, because modifications should be relatively minor.
1) **model.py:** Your p2 version should practically be the same. You can add batch normalization to fc1/fcs1 if you like.
2) **ddpg_agent.py:** You can play with (or add) the following:
```python
BUFFER_SIZE = between 1e5 and 1e6    # replay buffer size
LR_ACTOR    = between 1e-4 and 1e-3  # learning rate for the Actor
LEARN_EVERY = # learning timestep interval
LEARN_NUM   = # number of learning passes

```
#Ornstein-Uhlenbeck noise parameters
```python
OU_SIGMA    = #
OU_THETA    = #
EPSILON       = 1.0  # explore->exploit noise process (act step)
EPSILON_DECAY = 1e-6 # decay rate (learn step)
clip_grad_norm_()    # (learn step)
```
The above should hopefully get you going in the right direction. You just have to implement your training loop in your notebook. Good luck :shamrock:

*István:* Using batch size of 1024 helped a lot

*Ellyana Linden:* Last night, I was able to make my agent learned. I increased the LR for actor and critic to 2e-3 and reduced sigma to 0.1. I was so happy....but after around 300 episodes, the average score went down after its peak at 27.++ . It was 3 hours training :rolling_on_the_floor_laughing: 
Finally, I got 30 :slightly_smiling_face:
![final1](https://user-images.githubusercontent.com/14244685/73556293-5e2d9a80-4479-11ea-9d31-331ecc4e5079.jpg)

---

**Q3:** Trying second version challenge (20 agents) for more than 2 weeks. Need assistance! The average obtained goes up until it reaches over 30. So suddenly it starts to fall and not back to 30. Already using  clip grad norm and batch normalization. Tryed a lot of configurations for more than 48 hours training on GTX 1060. Any tip or suggestion? Thanks!
![image](https://user-images.githubusercontent.com/14244685/73556868-72be6280-447a-11ea-8cf9-3fe418390be3.png)

*Ellyana Linden:* I had the same problem. Mine reached 27 after that went down. What worked to me, decreased LR Actor and Critic, increased buffer size (this one is the key to my case), and I used sigma of 0.1. 

*Anna Scott:* I have used 1e-4  for learning rates for critic and actor. My sigma was 0.2.
int(1e5) was my buffer size.
I have trained locally on CPU and it took almost 4 hours.
The batch size made the difference for me, I made it 256.
The environment was solved in 912 episodes.

*Bruno Conterato:* Got it! 2 Attempts: one solved in a total of 125 episodes, the other 112. The main changes was Sigma to 0.1, and batch size of 128. I tried 256, but at the time other parameters were incorrect, then I had no result.

---

**Q4:** I have been trying to solve this challenge using the DDPG and code base of DDPG-pendulum. I used the same parameters and all the details unchanged except updating the environment. The reward is not crossing 0.1. Any ideas? I also tried with the parameters provided in the paper as well as taking reference from the above discussions from this channel. Still no luck.

*Ellyana Linden:* Try to change the hyperparameters value: 

---

Are the actor and critic supposed to have different learning rates? Is it better than them having the same? And if so, why?

Kinal  5 months ago
Nothing is a compulsion. You can experiment and use what works for you. As described in the project benchmark implementation of this project, DRL  "doesn't work yet". So its all experiment based. I also happened to notice that changing the random seed also make the difference of making or breaking of the models. For me same learning rate worked, but in the DDPG paper, they use different learning rates. So experiment and explore :stuck_out_tongue:

---

was struggling with hyperparameters and jumped into the second environment that used 20 instances and it worked better for me, however, I'm still stuck in a local minima around 5 score average, any advices ?

youben  8:03 PM
I finally managed to solve it in -47 episodes lol so we must keep it going for at least 100 episodes. The hyperparameters that I found impactful on the average score were: batch_size, buffer_size and sigma

---

Please can anyone help me understand the first quiz on Policy Gradient Quiz? The answer that was obtained doesn't makes sense to me.

ccquiel  4 months ago
The one in "What are Policy Gradient Methods" ?
The first one says that, because we want to output porbabailites for the actions, we should use a softmax activation function for the output layer.
Remember, Softmax is a function that takes as input a vector of real numbers, and normalizes it into a probability distribution.
The second one is about the policy gradient methods being a subset of policy methods. For example, Hill climbing is a type of policy method and the Gradient Policy method is also a type of policy methods. Both estimate the policy directly without using a Q-value function as intermediary.


---

Is there a code example somewhere of how to code the ddpg_agent.py for multiple agents for this project?


MSJose:car:  4 months ago
@Chris Palmer @Ellyana Linden The code for the 1-agent and 20-agents are identical, for both ddpg_agent.py and Continuous_Control.ipynb. The only difference is the UnityEnvironment file_name. Compared to the original files in ddpg-pendulum, the changes to ddpg_agent.py and Continuous_Control.ipynb are not very difficult, but are definitely non-trivial. For ddpg_agent.py, a trial-and-error approach would most certainly fail. For Continuous_Control.ipynb, you now need to track states, actions, rewards, dones, next_states, compared to the singular versions of these objects. I would say the changes to ddpg_agent.py are more challenging than to the Continuous_Control.ipynb itself. W.r.t. model.py, you can get away with not changing it, although a minor addition (for optimization) would help.

Chris Palmer  4 months ago
Thanks @MSJose. You've stated that the code changes between ddpg-pendulum and this project are non-trivial, yet there are no changes between handling 1 or 20 agents, I guess once the non-trivial changes are implemented!
It's therefore evident that I need help with what's needed for the differences between ddpg-pendulum and this project. I have code running, but no matter what parameters I have tried so far I never progress beyond 11.3. So, is that fact that I've got it running mean I've done the non-trivial bit, or have I failed to understand some core thing? Hmmm...

Ellyana Linden  4 months ago
If you can get score of 11.3, your code is running fine @Chris Palmer.Try tuning the hyperparameters.

Chris Palmer  4 months ago
Yes, trying that :slightly_smiling_face:. maybe there is something wrong in my implementation of batch normalization... any clues you can share in that regard?

MSJose:car:  4 months ago
@Chris Palmer W.r.t. model.py, stick with the 400/300 units for both Actor and Critic. Also, try batch normalization on only fc1 and fcs1 of Actor and Critic, respectively. See if that helps. With this project, IF you go over 500 episodes without convergence, there is something not totally right with your implementation.

MSJose:car:  4 months ago
@Chris Palmer Another thing you will find useful is 6. Benchmark Implementation, especially Attempt 3 and Attempt 4. Read through those, maybe a couple of times, and that will help you (if you haven't done the things mentioned there).

Chris Palmer  4 months ago
That does look useful. I've implemented point 3, can't figure out what to do for 4 though "At this point, we decided to get less aggressive with the number of updates per time step. In particular, instead of updating the actor and critic networks 20 times at every timestep, we amended the code to update the networks 10 times after every 20 timesteps. The corresponding scores are plotted below." Any advice?

Chris Palmer  4 months ago
[UPDATE] - figured this one out. Making progress, sort of, as now up to 19.3 but stuck there... Lots of experimentation required!
@MSJose - not sure how to do batch norm only on one layer. I set up my batch norm as self.bn1 = nn.BatchNorm1d(state_size). The only way that I've been able to work with that is to have a line like this at the beginning of the forward of the Actor and Critic: x = self.bn1(state). After that I am doing x = F.relu(self.fc1(x)). So, is that what you mean? I tried x = F.relu(self.bn1(self.fc1(state))) as suggested by the project tips, but that caused an error about array sizes. How would I set up my batch norm to work with that idea? (edited) 

Hugo Oliveira  4 months ago
@Chris Palmer I believe you are doing everything well, you just need to change the self.bn1 = nn.BatchNorm1d(state_size) to self.bn1 = nn.BatchNorm1d(output_of_your_fc1) because you want to normalize after you pass through your first fully connected layer.

Chris Palmer  4 months ago
Thanks @Hugo Oliveira. Yes, I worked that out... I've since found that my major issue is that I wasn't calculating my moving average correctly, so my model was doing well enough but I didn't realize it!

---

Hello everyone, I implemented project 2 based on the pendulum code, without changing the hyperparameters.
I'm always getting reward(and average score) equals to Zero.
Would someone please help me find what's wrong with the training loop below,
Thanks!
```python
def ddpg(n_episodes=500000, max_t=500, print_every=100):        
    scores_deque = deque(maxlen=print_every)
    scores = []
    for i_episode in range(1, n_episodes+1):
        env_info = env.reset(train_mode=True)[brain_name]
        state = env_info.vector_observations 
        ddpg_agent.reset()
        score = np.zeros(1)
        for t in range(max_t):
            action = ddpg_agent.act(state)
            env_info = env.step(action)[brain_name]
            next_state = env_info.vector_observations
            reward = env_info.rewards  
            done = env_info.local_done                       
            score += reward                      
            ddpg_agent.step(state, action, reward, next_state, done)
            state = next_state
            if done:
                break 
        scores_deque.append(score)
        scores.append(score)
        print('\rEpisode {}\tAverage Score: {:.4f}'.format(i_episode, np.mean(scores_deque)), end="")
        torch.save(ddpg_agent.actor_local.state_dict(), 'checkpoint_actor.pth')
        torch.save(ddpg_agent.critic_local.state_dict(), 'checkpoint_critic.pth')
        if i_episode % print_every == 0:
            print('\rEpisode {}\tAverage Score: {:.4f}'.format(i_episode, np.mean(scores_deque)))
            
    return scores  
```

Eka Antonius Kurniawan  3 months ago
You can try to lower noise sigma from 0.2 to 0.1.

Vova  3 months ago
Try reducing buffer_size, this may speed up training as well.

Kinal  3 months ago
If nothing works, try with the parameters which worked for others, but play around a little with the random seed:sweat_smile:

---

I have a question, why does it take longer time from episode to episode. Is it because the buffer? (for instance my 1st episode took 45sec and the number grows approximately 5sec every 10 episodes

MSJose:car:  3 months ago
@Eli Shay Yes, the increase in duration (per episode) is due to the saving to the replay buffer and the subsequent "learning" from it. If you recall, here's the code (loop) in Continuous_Control.ipynb.
In the 2nd loop, we run agent.step(), in which we call memory.add(), and then learn().
From the many runs I've made using the 20-agent version, the increase in duration (per episode) is roughly 2x from Episode 1 to the last episode when the environment is solved.
For example, in one run: 128/68 is about 1.88x
   Episode 1 (68s)    Mean: 0.0    Moving Avg: 0.0
   ...
   Episode 159 (128s)    Mean: 31.7    Moving Avg: 30.1
In another run: 115/56 is about 2.05x
   Episode 1 (56s)    Mean: 0.8    Moving Avg: 0.8
   ...
   Episode 105 (115s)    Mean: 38.8    Moving Avg: 30.2
NOTE: In the 1-agent version, the increase in duration (per episode) from 1st episode to last is not as much, just about 1.6x.
Let us know about your experience on p2 so we learn from it as well. Cheers :champagne:
   for i_episode in range(1, n_episodes+1):
       ...
       for t in range(max_t):
           ...
           # save experience to replay buffer, perform learning step at defined interval
           for state, action, reward, next_state, done in zip(states, actions, rewards, next_states, dones):
               agent.step(state, action, reward, next_state, done, t, num_agents, accumulate=False)
           ...
   def step(self, state, action, reward, next_state, done, timestep):
       """Save experience in replay memory, and use random sample from buffer to learn."""
       # Save experience / reward
       # If updating in batches, then add the last memory of the agents (e.g. 20 agents) to a buffer
       # and if we've met batch size only push to learn in multiples of whatever LEARN_NUM specifies (e.g.10)
       self.memory.add(state, action, reward, next_state, done)
       # Learn, if enough samples are available in memory
       if len(self.memory) > BATCH_SIZE and timestep % LEARN_EVERY == 0:
           for _ in range(LEARN_NUM):
               experiences = self.memory.sample()
               self.learn(experiences, GAMMA) (edited) 




Wira  3 months ago
@Eli Shay Another possible reason is because it is episodic
In the beginning of training it would be fast because the agent would take a bad decision that caused the environment to stop (done = True)
But later on when the agents get better, it would be able to maintain a longer episode, hence a longer epoch.
This is of course related to saving experiences to replay buffer too
I hope it helps
Thanks








---


---


Ioannis Anifantakis  

![image](https://user-images.githubusercontent.com/14244685/73572480-1a4b8d00-449b-11ea-9d4f-47e8482076e9.png)
The above results refer to the exactly same architecture with the exact same hyperparams. You can clearly see how faster and efficient the 20 Agents approach is compared to the 1 Agent approach.
So may I suggest you guys go directly for the 20 agents solution, as it will train much easier and faster.


## Tips from *MSJose*

**Rubric Requirements:**

* [v1] the agent receives an average reward (over 100 episodes) of at least +30, or
* [v2] the agent is able to receive an average reward (over 100 episodes, and over all 20 agents) of at least +30.

**Current Result using DDPG:** Solved in 15 episodes (30.0). Not sure if this is good or bad because the *6. Benchmark Implementation* topic doesn't state the minimum number of episodes to achieve the +30 (over 100 episodes) score. For this project, I tried Version 2: Twenty (20) Agents as it looked more interesting. As suggested in that topic, we are encouraged to explore TRPO, TNPG, PPO, or the very recent D4PG algorithm - after trying DDPG.

**A note about this project:** the agent takes a *l-o-n-g* time to train. Even on my local Ubuntu setup with a GTX 1070 GPU, training took 3.5 hours. In the Udacity Workspace (with GPU) which is slower, it will take even more time. It's good we are given 168 hours of GPU time.

![image_720](https://user-images.githubusercontent.com/14244685/73551725-215da580-4471-11ea-8f36-ae925771978a.png)


**(Optional) Challenge: Crawl**

After completing the *p2_continuous-control project*, I felt lucky :grinning: so decided to try this challenge. The blurb states this is "a more difficult continuous control environment, where the goal is to teach a creature with four legs to walk forward without falling".
Similar to the 1st (optional) challenge, this one has no benchmark implementation. It's a *fun* challenge to do; not too difficult, and not too long to train (less than 1 hour on my GTX 1070).

Here is my first try. Cheers!

![image](https://user-images.githubusercontent.com/14244685/73552096-cf694f80-4471-11ea-8558-e106b61ec2c3.png)

## Tips from *Reham El-Kholy*

Not bad for a single agent :smile: 

I used DDPG even though it's so unstable. But what really did it was tuning sigma (the standard deviation) for the noise. It took less than an hour to train.

![image](https://user-images.githubusercontent.com/14244685/73552677-df356380-4472-11ea-9418-e51dc5c2366e.png)




## Tips from *Andrei Li*

Watch out training loop and check it twice, otherwise, you will be with advanced tuning tutorials for reinforcement learning when the problem is in training loop. 

Two cases are important: 
1) Score is constantly close to 0.0 and 
2) Score is not growing beyond a specific level.


Kiril Cvetkov  7:03 PM
Use ELU instead RELU :slightly_smiling_face: from my experience, it oftenly provides more stable training for actor-critic problems. Solved the second environment in 105 epochs  :slightly_smiling_face:
