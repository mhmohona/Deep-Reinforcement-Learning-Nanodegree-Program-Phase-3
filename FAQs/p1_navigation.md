
**Q1: Though, I do not make progress enough but from curiosity I want to know, Is it possible to do the projects in google colab?** 

*Ajit Kale:* I have written this a year ago, ask if something is not coherent today - [Reinforcement Learning on google colab](https://medium.com/@kaleajit27/reinforcement-learning-on-google-colab-9cb2e1ef51e)


**Q2: Do we need C++ for this project?**

*Sabrina Palis:* I was a bit confused about it too, because we were prompted to learn C++ at the beginning of the lessons of part 2. I checked the project submission requirements: "The code is written in PyTorch and Python 3." :sweat_smile:

**Q3: Is anyone else having trouble setting up the environment? I'm running Win 10 x64, and I keep getting "No module named unityagents" when trying to run the python code. I've uninstalled and reinstalled Anaconda and gone through all the instructions over and over again and can't get it working. Any ideas would be appreciated.**

*MSJose:* I've always used from unityagents import UnityEnvironment. Running unityagents==0.4.0 on Ubuntu 18.04.2 LTS. If it's running properly on your env, I guess it's OK. Also, mlagents==0.9.0 and mlagents-envs==0.9.0

**Q4: hello every one  i have error between pyhton API and Unity API " The API number is not compatible between Unity and python. Python API : API-9, Unity API : API-4. " this message appears after opening unity for few seconds any clue how to solve it ?? PS using ubuntu 16**

*MSJose:* I am running Unity-2018.2.3f1. Here are what I have on my local Ubuntu 18.04.3 LTS setup.

atari-py==0.2.6

box2d-py==2.3.8

gym==0.14.0

Keras==2.1.6

matplotlib==2.1.0

mlagents==0.9.0

mlagents-envs==0.9.0

mujoco-py==2.0.2.4

numpy==1.14.5

pandas==0.25.0

Pillow==5.4.1

protobuf==3.6.1

pyglet==1.3.2

pytest==3.10.1

PyYAML==5.1.2

qtconsole==4.5.2

six==1.12.0

tensorflow==1.7.1

tensorflow-gpu==1.7.1

torch==0.4.0

torchvision==0.2.1

unityagents==0.4.0

I think they should work on 16.04 as well, but you'll have to check and verify. Hopefully this helps.

**Q5: Can anyone explain how to interpret the rubric "Plot of Rewards"? Is this different from the plot we produce when doing the training?
I don't understand why it says the plot should "illustrate that the agent is able to receive an average reward (over 100 episodes) of at least +13" - I cannot even get over 13 rewards in just 100 consecutive episodes - the best I can do if I run my trained model is 15 over 300 episodes, and that is not an average its an accumulated score...
Besides which, if I try to run 100 episodes without including the if done: break then I get an error - so the environment itself doesn't permit me to run 100 episodes with a score of 13 per episode!**

*MSJose:* It basically means you run your training for say, num_episodes == 2500, and then you take the average score, called the moving average, over the last 100 episodes. If this average is >= the target average of 13.0, then you stop training and you report your environment solved in current_episode - 100. Hope that helps.

**Q6: Hey guys, i am trying to run the dqn algorithm but it keeps throwing an error saying that the episode is completed. I tried doing the reset but it still doesnt work.**

*Kinal:* the environment returns if the episode is done or not so you can add to your code

 `if done:
    break`
    
you can check if the episode is done or not using

`done = env_info.local_done[0]`

*Jon Hasan:* I think i got it. The env info variable had to be inside the for loop. I am getting a plot of the episodes but they are not showing improvement.

**Q7: Hi all, I have a question. I have trained my model with good results:**

**Episode 100    Average Score: 12.68**

**Episode 131    Average Score: 15.00**

**Environment solved in 31 episodes!    Average Score: 15.00**

**But when I test it, it does not even get one single banana. I don't understand...**

**Episode 1    Average Score: 0.00**

**Episode 2    Average Score: 0.00**

**Episode 3    Average Score: 0.00**

**Episode 4    Average Score: 0.00**

**Episode 5    Average Score: -0.20**

**Episode 6    Average Score: -0.17**

**Episode 7    Average Score: -0.14**

**Episode 8    Average Score: -0.12**

**Episode 9    Average Score: -0.11**

**Episode 10    Average Score: -0.20**

**The checkpoint file is always the same size, is there something wrong?**

*MSJose:* Sub-200 solutions are quite good already, but sub-100 solutions are fantastic! When you test the saved agent, you should normally see an average score > 13.0 right at Episode 1. Review your code w.r.t. computing the moving average over the last 100 episodes. Good luck :shamrock:
You have a scores_window of length 100 where you append your episode score. At each episode, you compare the mean of this scores_window with your target score. IF this mean is >= your target score, then you save your state_dict, display the environment solved in current episode # - 100, and you exit the loop. 


**Q8: Guys, another question about the p1, the instruction says: to solve this environment, you will need to design a convolutional neural network as the DQN architecture. Do we really need a CNN?**

*MSJose:* No, you don't need a CNN. (To clarify, you just need the Linear layers; no need for Conv2d or Conv3d.)

**Q9: Just wondering, are the model architectures supposed to be complex for this project?
I am trying to use two conv layers and two fully connected layers.**

*MSJose:* Just re-read the topic 7. Not sure where to start? and follow Steps 2-4. You don't need to sweat this out :smiley: Good luck :shamrock:

**Q10: i used the reference code from the workspace in the dqn module. However, my model isnt even reaching 1 after 1000 episodes. This is a hyperparameter issue?**

*MSJose:* (1) If you did, you would have copied both dqn_agent.py and model.py from the DQN solution. You do not need to modify these 2 files. (2) The only code changes you need to do are in Navigation.ipynb. There are exactly (a minimum of) 6 lines of code you need to add and/or update to make it work - all within the dqn() function which you need to copy from the Deep_Q_Network_Solution notebook.  (3) If you do #2 above correctly, you can solve the environment in about 500 episodes, using the default parameters. Hopefully these are good enough to get you going. Again, good luck :shamrock:

**Q11: Hi everyone, I have successfully installed the pytorch and the drlnd environment - however, the "Banana.exe" simulator is not working on Windows 10. It freezes and gives the message "the progrom does not respond. Any hint. Thanks.**

*Kinal:* You can ignore that message and keep running next cells in Jupiter notebook. It'll start running.

**Q12: I'm using Ubuntu 18.04, insallation is fine. I can import UnityEnvironment.
But when i run `env = UnityEnvironment(file_name="Banana_Linux/Banana.x86_64")` i get a new window open sayin "made with unity" and then "Banana_x86_64 is not responding".
and when i run `env_info = env.reset(train_mode=True)[brain_name]` , it takes forever.** 

*MSJose:*  I have been running the DRLND code in Ubuntu 18.04.3 LTS since Day 1 and have not encountered any problems.

Here's a partial snapshot of my environment:

atari-py==0.2.6

box2d-py==2.3.8

graphviz==0.12

gym==0.10.11

gym-retro==0.7.0

JSAnimation==0.1

matplotlib==2.1.0

mlagents==0.9.0

mlagents-envs==0.9.0

numpy==1.16.0

pandas==0.24.0

progressbar==2.5

pybullet==2.5.5

qtconsole==4.5.2

tensorboard==1.7.0

tensorboardX==1.8

tensorflow==1.7.1

tensorflow-gpu==1.7.1

tensorflow-tensorboard==0.1.5

torch==1.2.0

torchsummary==1.4

torchvision==0.4.0

unityagents==0.4.0

Try to check if there's any conflict with your packages.

After you run the ff. line of code,

`env = UnityEnvironment(file_name="/home/sentinel/Banana_Linux/Banana.x86_64")`

you will see the "Made with Unity" logo, and then the following display on your notebook:

INFO:unityagents:

'Academy' started successfully!

Unity Academy name: Academy
       Number of Brains: 1
       Number of External Brains : 1
       Lesson number : 0
       Reset Parameters :
        
Unity brain name: BananaBrain
       Number of Visual Observations (per agent): 0
       Vector Observation space type: continuous
       Vector Observation space size (per agent): 37
       Number of stacked Vector Observation: 1
       Vector Action space type: discrete
       Vector Action space size (per agent): 4
       Vector Action descriptions: , , ,


**Q13: Mmmh, I think I missed something during the lesson but going back on my project submission, I was wondering:
why are we removing 100 episodes from the total count when the environment is solved? :thinking_face:
I understand we have a running average, but at least shouldn't we consider that if the running average is above the threshold, then the average episode when it was solved is somewhere in the middle? (meaning episode_idx - 50)
Given that, hopefully, your score is increasing during training on average. If we take the beginning episode corresponding to running_avg_score=13, then most likely, at this specific episode, the agent was not already able to reach that score consistently :man-shrugging:**

*Ioannis Anifantakis*

Answer:
We don't achieve goal by just having an episode reaching our goal, but by having 100 consecutive episodes scoring above our score by average!

Example:
If by episode 300 the average of the last 100 episodes exceed my goal, it means that by about episode 200 I normally should have achieved my goal. :wink:

PS I also removed it on my first 2 projects, but hey on my 3rd project I held the -100 score to make my overall episodes seem less and more impressive :smile:


---



### Tips from *Ioannis Anifantakis*

*(The reason I posted it in project 1 channel, is because we use Fixed-Q-Targets in our project)* :wink:

Made a **Fixed Q-Targets** GIF to help visualize the concept of the 2 replicas (local and target) DQNs when it comes to training Neural Networks in Reinforcement Learning.

You are an online model (you produce, with each consecutive move, your own training dataset - "on the go").

You make some discoveries based on your existing weights. So you have to produce new weights based on your existing weights discoveries. You really try to improve yourself, using "yourself". This won't really work...

You need to keep your distances and use a target network that is your replica, and then use this network as the target based on which you make your changes. After a few steps, you just sync the two networks again and keep going.

I always saw the single network as a visualization of being inside a wooden raft, blowing at it, hoping it will "move"... which simply... doesn't work! Instead, you had to take your distance with a replicated network based on which you train some batches (which works!), then after this number of batches sync again the networks and keep going.

Hope this visualization helps!

![Fixed-Q-Network](https://user-images.githubusercontent.com/14244685/72685494-eb393100-3b14-11ea-8ab5-98ba6598614c.gif)


### Tips from *MSJose* -

**Rubric Requirements:** 

* Avg. Reward (over 100 episodes) at least 13+. 

* Solve the environment in < 1800 episodes. Current Result using DQN: Solved in 310 episodes (13.02). Now to try and improve via hyperparameter tuning and later using Double DQN, Dueling DQN, and PER (Prioritized Experience Replay). This will indeed be an exciting couple of months :grinning:

* Once you start training your agents, you will notice one thing: reproducibility is not guaranteed; i.e., you will most likely get a different result between runs, sometimes by a wide margin. That's just RL :grinning:

Greetings, fellow Survivors! This post is for the (roughly) 75% of you who have not started, or are just starting, with the p1_navigation project. I created an easy, tested, 12-step hands-on guide for this first project. The guide is a fleshed-out version of the two infographics already out there. There's no actual code in the guide. (If there is, where is the fun :smiley:)

If you follow all the steps correctly, you should be able to solve the environment in 400-500 episodes, even using just the _default param-value pairs. Guaranteed!

With the guide, you can complete the project in 1-2 hours, perhaps even less, by just adding/updating exactly 6 lines of code.

Anyway, feel free to use it. (Don't worry, I have cleared it with our DRLND CM.)

Finally, since the guide is (embarrassingly) easy to follow, I won't answer any questions about it :grin:

Of course, you can do the project any way you want; I thought I'd just help free up some of your precious time for the more challenging p2 and p3 projects.

Cheers :champagne: and good luck :shamrock:

So here it is: 


1. In the p1_navigation folder, duplicate Navigation.ipynb to, say, Navigation_WIP.ipynb.
   * Replace the file_name="..." (in UnityEnvironment()) with the appropriate value corresponding to your environment.
2. From the P2.L02.dqn/solution folder, copy Deep_Q_Network_Solution.ipynb (for reference) *AND* dqn_agent.py and model.py to p1_navigation.
   * You do *NOT* need to modify the two .py files.
3. In Navigation_WIP.ipynb, comment out the *env.close()* line, or delete the cell containing it.
4. At the bottom of Navigation_WIP.ipynb, add the necessary imports:
   * torch, matplotlib, collections (for deque)
5. Add import Agent (from dqn_agent)
6. From Deep_Q_Network_Solution.ipynb, copy the _whole_ *def dqn(...)* function.
   * The code changes to make the solution work are all _within_ this function.
7. There are *_exactly_* 6 lines you need to add and/or update in dqn().
   * Get state from env_info        (2 lines)
   * Get next_state from env_info   (2 lines)
   * Get reward, done from env_info (2 lines)
   * DO NOT FORGET to change the value in *if np.mean(scores_window)>=200.0:* to 13.0!
8. (OPTIONAL) If you want to plot moving_avg, you need to add exactly 3 lines within dqn():
   * Initialize moving_avg as an empty list.
   * Append the mean of the last 100 scores to moving_avg AFTER every episode.
   * Return moving_avg from dqn() for plotting purposes.
9.  Create agent from Agent(), passing the appropriate param-value pairs.
10. Generate scores (or scores, averages) from dqn(), passing the *_default_* param-value pairs.
11. At the very bottom, below your plotting code, add env.close().
12. Execute the notebook using "Run All".
    * If you did all the steps above _correctly_, you should see the training results being displayed per episode, and should see convergence well within the default n_episodes=2000, even using just the _default_ param-value pairs.
==================================================
13. Once your solution IS running, converging, and plotting, duplicate Navigation_WIP.ipynb to, say, Navigation_Final.ipynb.
14. Do your parameter tuning on Navigation_Final.ipynb.
    * REMEMBER: Unless you are using automated parameter-optimization code, change your parameters one at a time and note/record the effect whether it improves or worsens the performance of your agent.
15. For your reference, I ran the solution above 5 times using the _default_ param-value pairs.
    * The model converged in 448, 348, 464, 464, and 423 episodes, respectively, for an average of 429.
    * Each complete run took less than 10 mins. on an 8GB GTX 1070 GPU (Ubuntu 18.04.3 LTS, local).
16. WHAT TO WATCH FOR
    * IF your training runs for the default 2000 episodes without converging, there is *_most probably_* something wrong with your dqn() implementation.
17. STRETCH GOAL: Beat 138 episodes!
    * That's the best convergence I got from about a couple of hours tuning.
    * BUT, you don't have to do this... anything in the 300-400 range should be good enough.`


**(Optional) Challenge: Learning from Pixels**

Inspired by @Kiril Cvetkov, I decided to tackle this. Big mistake :sweat_smile: This challenge is not only harder; it really takes longer to train than p1_navigation. Here the agent needs to learn directly from pixels, where the state is an 84x84 RGB image.
Anyway, here is my result, after working on it the whole day and training for 5+ hours (with GPU). There is a note in the blurb that says "it is not possible to train this agent in the provided Udacity Workspace", but I didn't try.

**Disclaimer:** This is my 1st try, so I have no idea if it's good enough or really bad. There's no benchmark implementation. I just assumed that the goal is (the same) 13+ over a period of 100 episodes. It's an interesting challenge, so I might come back to this after graduation.
Cheers!

![1](https://user-images.githubusercontent.com/14244685/72685300-06a33c80-3b13-11ea-9073-28044fe26532.png)
