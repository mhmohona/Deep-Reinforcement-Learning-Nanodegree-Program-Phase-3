## In General FAQs: 

**[FOR WINDOWS users - setting up the drlnd environment]**
*Sabrina Palis:* I was struggling setting up the drlnd environment on Windows. 
If you get stuck and unable to set up Box2D this may help:

`conda install swig` # needed to build Box2D in the pip install

`pip install box2d-py` # a repackaged version of pybox2d

If you get an error message about torch==0.4.0, check out this page:
https://github.com/udacity/deep-reinforcement-learning/issues/13

---

**Q:** Which step do you take first in improving the performance of the agent? Adding the nodes of fully connected layers or tuning the hyperparameters? Which hyperparameters do you think that will provide significant effect in an agent’s performance as there are lots of hyperparameters in Deep Reinforcement Learning? Do you have any guideline of hyperparameters tuning? 

*Alessandro Restagno:* 
* The first thing I do, it's usually trying different learning rates. Let's say 0.01 / 0.001 / 0.0001.
* Neural networks don't usually make a big difference in these projects. You can try to add an hidden layer and see, if there is a significant improvement.
* After the learning rate, I think that two important parameters are Buffer Size and Batch Size.
