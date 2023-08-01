# COMCAST Innovation Fund: DDPG plugin for MPCC

In this module, we design and implement pluggable DDPG into MPCC and compare results with the vanilla MPCC. 

## Description

We present a novel experience-driven MPCC (Multipath Performance oriented Congestion Control) approach, which is a novel Deep Learning based architecture for high-performance multipath congestion management. Our solution employs Deep Deterministic Policy Gradient (DDPG) with online convex optimization to achieve the impeding joint pursuits of fairness and exemplary performance in challenging multipath congestion control contexts. In our experimental tests with a kernel implementation over realistic network settings, the proposed DDPG-MPCC surpasses state-of-the-art MPTCPs. In testing with a kernel implementation on simulated networks, the proposed DDPG-MPCC surpasses state-of-the-art data protocols by a wide margin. 

- rlinputdata.csv : This contains infomation about various environment condition and transmission rates while running MPCC. This will allow us to train our DDPG model to choose the most optimium rate in a particular environment.

- DDPG_train.ipynb : This file trains the DDPG model for 100 episodes and save the results in avg_reward_list.csv,new_states_dict.pkl and states_record.pkl

- DDPG_gen_graph.ipynb : This generates three graphs based on data we get from our training session.

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

* Install python on your systems (Annaconda is easy to configure the versions of python and installed libraries)

OR

* You can upload rlinputdata.csv and DDPG_train.ipynb to google colab or use Jupyter notebooks

Then,

Install dependent libraries for running the python notebook.

### Executing program

* Execute Run all to execute both DDPG_train.ipynb and then DDPG_gen_graph.ipynb



## Investigators

- [Shiva Pokhrel](https://www.deakin.edu.au/about-deakin/people/shiva-pokhrel) <shiva.pokhrel@deakin.edu.au>
- Jonathan Kua <jonathan.kua@deakin.edu.au>
- Deol Satish <dsatish@deakin.edu.au>
- Sebnem Ozer (COMCAST, Charter)
- Anwar Walid (Amazon Science)

## References

[1] Gilad, Tomer, Neta Rozen-Schiff, P. Brighten Godfrey, Costin Raiciu, and Michael Schapira. "MPCC: online learning multipath transport." In Proceedings of the 16th International Conference on emerging Networking EXperiments and Technologies, pp. 121-135. 2020.

[2] S. R. Pokhrel and A. Walid, "[Learning to Harness Bandwidth with Multipath Congestion Control and Scheduling](https://ieeexplore.ieee.org/abstract/document/9444785)," in IEEE Transactions on Mobile Computing, 2021, doi: 10.1109/TMC.2021.3085598 
