As a part of the **PyTorch scholarship**, those who got the scholarship were in a slack Workspace.
Here I have jotted down questions have been asked there in slack and answers given by other scholarship holders hoping it will be easier for me when I will revice course content in future. As well as maybe some other will find it benificial. 


## General FAQs: 

![DRLND Projects Tips](https://user-images.githubusercontent.com/14244685/73575709-f2602780-44a2-11ea-81c7-26083fcde84d.png)


**[FOR WINDOWS users - setting up the drlnd environment]**
*Sabrina Palis:* I was struggling setting up the drlnd environment on Windows. 
If you get stuck and unable to set up Box2D this may help:

`conda install swig` # needed to build Box2D in the pip install

`pip install box2d-py` # a repackaged version of pybox2d

If you get an error message about torch==0.4.0, check out this page:
https://github.com/udacity/deep-reinforcement-learning/issues/13

---

**Q1:** Which step do you take first in improving the performance of the agent? Adding the nodes of fully connected layers or tuning the hyperparameters? Which hyperparameters do you think that will provide significant effect in an agent’s performance as there are lots of hyperparameters in Deep Reinforcement Learning? Do you have any guideline of hyperparameters tuning? 

*Alessandro Restagno:* 
* The first thing I do, it's usually trying different learning rates. Let's say 0.01 / 0.001 / 0.0001.
* Neural networks don't usually make a big difference in these projects. You can try to add an hidden layer and see, if there is a significant improvement.
* After the learning rate, I think that two important parameters are Buffer Size and Batch Size.

---

**Q2:** When I work on Udacity workspace using GPU or even without GPU, the kernel got disconnected in the middle of the training session. I can't even finish a training session to the end. Any once faced this problem before? any available solution?

*RJ:*
@wafarag Now that I started working on 'Project 2,' I realize that modifying my 'Screen timeout settings' was not enough to prevent my workspace from disconnecting after 30 minutes of idleness. To prevent that from happening, I had to implement Udacity's recommendation found her: https://udacity.zendesk.com/hc/en-us/articles/360019820872-What-do-I-do-if-my-instance-keeps-quitting-


So for the sake of people that will try to understand:

if you somehow can't reproduce the results from your workspace locally, I figured that the compiled environment is not the same as the one available for download. I was trying to reproduce results with same seed but had troubles getting the same thing: the troublemaker was the difference in the compiled version of the environment :sweat_smile:
I happen to have had to finish the ND this week, so I trained in parallel p2 and p3 (one locally the other on udacity workspace), that's how I figured it 



