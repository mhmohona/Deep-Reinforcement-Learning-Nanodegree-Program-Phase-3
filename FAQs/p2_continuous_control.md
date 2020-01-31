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


---

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

