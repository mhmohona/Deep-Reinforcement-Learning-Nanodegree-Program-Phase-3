
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


#### Tips from *MSJose* -

**Rubric Requirements:** 

* Avg. Reward (over 100 episodes) at least 13+. 

* Solve the environment in < 1800 episodes. Current Result using DQN: Solved in 310 episodes (13.02). Now to try and improve via hyperparameter tuning and later using Double DQN, Dueling DQN, and PER (Prioritized Experience Replay). This will indeed be an exciting couple of months :grinning:

* Once you start training your agents, you will notice one thing: reproducibility is not guaranteed; i.e., you will most likely get a different result between runs, sometimes by a wide margin. That's just RL :grinning:


**(Optional) Challenge: Learning from Pixels**

Inspired by @Kiril Cvetkov, I decided to tackle this. Big mistake :sweat_smile: This challenge is not only harder; it really takes longer to train than p1_navigation. Here the agent needs to learn directly from pixels, where the state is an 84x84 RGB image.
Anyway, here is my result, after working on it the whole day and training for 5+ hours (with GPU). There is a note in the blurb that says "it is not possible to train this agent in the provided Udacity Workspace", but I didn't try.

**Disclaimer:** This is my 1st try, so I have no idea if it's good enough or really bad. There's no benchmark implementation. I just assumed that the goal is (the same) 13+ over a period of 100 episodes. It's an interesting challenge, so I might come back to this after graduation.
Cheers!

![1](https://user-images.githubusercontent.com/14244685/72685300-06a33c80-3b13-11ea-9073-28044fe26532.png)
