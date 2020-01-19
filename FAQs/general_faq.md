## In General FAQs: 

**[FOR WINDOWS users - setting up the drlnd environment]**
*Sabrina Palis:* Hey guys, I was struggling setting up the drlnd environment on Windows. 
If you get stuck and unable to set up Box2D this may help:

conda install swig # needed to build Box2D in the pip install

pip install box2d-py # a repackaged version of pybox2d

If you get an error message about torch==0.4.0, check out this page:
https://github.com/udacity/deep-reinforcement-learning/issues/13
