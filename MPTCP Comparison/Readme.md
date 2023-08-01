# Project COMCAST Innovation Fund

DDPG-MPCC: Experience Driven Multipath Performance Oriented Congestion Control

## Description

We design, implement and  present an experience-driven MPCC (Multipath Performance oriented Congestion Control) approach, which is a novel Deep Learning based architecture for high-performance multipath congestion management. Our solution employs Deep Deterministic Policy Gradient (DDPG) with online convex optimization to achieve the impeding joint pursuits of fairness and exemplary performance in challenging multipath congestion control contexts. In our experimental tests with a kernel implementation over realistic network settings, the proposed DDPG-MPCC surpasses state-of-the-art MPTCPs. In testing with a kernel implementation on simulated networks, the proposed DDPG-MPCC surpasses state-of-the-art data protocols by a wide margin. See all three readme files.

## Getting Started

Clone this repository first.

### Dependencies

* Python v3.9.13 or Higher

Libraries required:
* numpy - v1.23.3
* matplotlib -v3.5.2
* pandas - v1.4.4

### Installing

* Install python on your systems (Annaconda is easy to configure the versions of python and installed libraries)

OR

* You can upload results-trialc.txt.csv,results-triald.txt and results-triale.txt from bandwidthdata and losspercentagedata folder into another folder with same name respectively and graph_buffer.ipynb and graph_loss.ipynb to google colab or use Jupyter notebooks.

* To run ddpg_data_gen.ipynb, you need rldata.txt which you extract from kernel logs in the client node.

Then,

Install dependent libraries for running the python notebook.

### Executing program

* Execute Run all to execute both graph_buffer.ipynb and graph_loss.ipynb and ddpg_data_gen


## Investigators:
 [Shiva Pokhrel](https://www.deakin.edu.au/about-deakin/people/shiva-pokhrel) <shiva.pokhrel@deakin.edu.au>
- Jonathan Kua <jonathan.kua@deakin.edu.au>
- Deol Satish <dsatish@deakin.edu.au>


## References

[1] Gilad, Tomer, Neta Rozen-Schiff, P. Brighten Godfrey, Costin Raiciu, and Michael Schapira. "MPCC: online learning multipath transport." In Proceedings of the 16th International Conference on emerging Networking EXperiments and Technologies, pp. 121-135. 2020.

[2] S. R. Pokhrel and A. Walid, "Learning to Harness Bandwidth with Multipath Congestion Control and Scheduling," in IEEE Transactions on Mobile Computing, 2021, doi: 10.1109/TMC.2021.3085598 

