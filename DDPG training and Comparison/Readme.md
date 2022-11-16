# Project Title

In this we run our DDPG and compare results with MPCC.

## Description

*-rlinputdata.csv : This contains infomation about various environment condition and transmission rates while running MPCC. This will allow us to train our DDPG model to choose the most optimium rate in a particular environment.

*-DDPG_train.ipynb : This file trains the DDPG model for 100 episodes and save the results in avg_reward_list.csv,new_states_dict.pkl and states_record.pkl

*-DDPG_gen_graph.ipynb : This generates three graphs based on data we get from our training session.

## Getting Started

Clone this repository first.

### Dependencies

* Python v3.9.13 or Higher

Libraries required:
* gym - v0.21.0
* tensorflow - v2.8.2
* keras - v2.8.0
* numpy - v1.23.3
* matplotlib -v3.5.2
* pandas - v1.4.4



### Installing

*Install python on your systems (Annaconda is easy to configure the versions of python and installed libraries)

OR

*You can upload rlinputdata.csv and DDPG_train.ipynb to google colab or use Jupyter notebooks

Then,

Install dependent libraries for running the python notebook.

### Executing program

* Execute Run all to execute both DDPG_train.ipynb and then DDPG_gen_graph.ipynb
```



