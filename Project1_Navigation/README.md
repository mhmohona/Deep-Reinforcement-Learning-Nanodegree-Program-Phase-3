# Environment

For this project, I have traind an agent to navigate (and collect bananas!) in a large, square world. 

![banana](https://user-images.githubusercontent.com/14244685/65367971-ca8ec680-dc5b-11e9-9e63-17c5739c302a.gif)

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:

- `0` - move forward.

- `1` - move backward.

- `2` - turn left.

- `3` - turn right.

The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.


_Follow the instructions below to explore the environment on your own machine! You will also learn how to use the Python API to control your agent._

## Step 1: Clone the DRLND Repository
If you haven't already, please follow [the instructions in the DRLND GitHub repository](https://github.com/udacity/deep-reinforcement-learning#dependencies) to set up your Python environment. These instructions can be found in `README.md` at the root of the repository. By following these instructions, you will install PyTorch, the ML-Agents toolkit, and a few more Python packages required to complete the project.

(For Windows users) The ML-Agents toolkit supports Windows 10. While it might be possible to run the ML-Agents toolkit using other versions of Windows, it has not been tested on other versions. Furthermore, the ML-Agents toolkit has not been tested on a Windows VM such as Bootcamp or Parallels.

## Step 2: Download the Unity Environment
For this project, you will not need to install Unity - this is because we have already built the environment for you, and you can download it from one of the links below. You need only select the environment that matches your operating system:

Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)

Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)

Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)

Then, place the file in the `p1_navigation/` folder in the DRLND GitHub repository, and unzip (or decompress) the file.


(For AWS) If you'd like to train the agent on AWS (and have not enabled a virtual screen), then please use [this link](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md) to obtain the "headless" version of the environment. You will not be able to watch the agent without enabling a virtual screen, but you will be able to train the agent. (To watch the agent, you should follow the instructions to enable a [virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md), and then download the environment for the Linux operating system above.)

# Step 3: Explore the Environment
After you have followed the instructions above, open `Navigation.ipynb` (located in the `p1_navigation/ folder` in the DRLND GitHub repository) and follow the instructions to learn how to use the Python API to control the agent.

Watch the (silent) [video](https://youtu.be/ltz2GhFv04A) to see what kind of output to expect from the notebook, if everything is working properly!

# _(Optional)_ Build your Own Environment
For this project, we have built the Unity environment for you, and you must use the environment files that we have provided.

If you are interested in learning to build your own Unity environments after completing the project, you are encouraged to follow the instructions [here](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Getting-Started-with-Balance-Ball.md), which walk you through all of the details of building an environment from a Unity scene.


#Implementation

#future work


'''
a README that describes how someone not familiar with this project should use your repository. 
The README should be designed for a general audience that may not be familiar with the Nanodegree program; 
you should describe the environment that you solved, along with how to install the requirements before running the 
code in your repository.
the code that you use for training the agent, along with the trained model weights.
a report describing your learning algorithm. This is where you will describe the details of your implementation, 
along with ideas for future work.
'''
