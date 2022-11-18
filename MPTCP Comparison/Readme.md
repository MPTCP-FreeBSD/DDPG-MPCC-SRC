# Project Title

Extending MPCC: Learning FRom Experience

## Description

In this part of the codebase, we gather data from our cloudlab testbed and run visual comparisons to draw conclusions on the performance of various mptcp algorithms
and extract data required for training DDPG Model

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

- Shiva Raj Pokhrel <shiva.pokhrel@deakin.edu.au>
- Jonathan Kua <jonathan.kua@deakin.edu.au>
- Deol Satish <dsatish@deakin.edu.au>



