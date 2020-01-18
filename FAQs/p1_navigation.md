
**Q1: Though, I do not make progress enough but from curiosity I want to know, Is it possible to do the projects in google colab?** 

*Ajit Kale:* I have written this a year ago, ask if something is not coherent today - [Reinforcement Learning on google colab](https://medium.com/@kaleajit27/reinforcement-learning-on-google-colab-9cb2e1ef51e)


**Q2: Do we need C++ for this project?**

*Sabrina Palis:* I was a bit confused about it too, because we were prompted to learn C++ at the beginning of the lessons of part 2. I checked the project submission requirements: "The code is written in PyTorch and Python 3." :sweat_smile:

**Q3: Is anyone else having trouble setting up the environment? I'm running Win 10 x64, and I keep getting "No module named unityagents" when trying to run the python code. I've uninstalled and reinstalled Anaconda and gone through all the instructions over and over again and can't get it working. Any ideas would be appreciated.**

*MSJose:* I've always used from unityagents import UnityEnvironment. Running unityagents==0.4.0 on Ubuntu 18.04.2 LTS. If it's running properly on your env, I guess it's OK. Also, mlagents==0.9.0 and mlagents-envs==0.9.0




**Tips from *MSJose* -**
Rubric Requirements: (1) Avg. Reward (over 100 episodes) at least 13+. (2) Solve the environment in < 1800 episodes. Current Result using DQN: Solved in 310 episodes (13.02). Now to try and improve via hyperparameter tuning and later using Double DQN, Dueling DQN, and PER (Prioritized Experience Replay). This will indeed be an exciting couple of months :grinning:
