[__Back to home__](index.md)

# Getting Started

## Anaconda

Firstly install Anaconda by following the guide [here](https://docs.anaconda.com/anaconda/install/)

### Creating an Anaconda virtual environment

It is necessary to create a virtual environment when running a project in order to keep all your dependencies (in our case python library versions) isolated from other versions of the packages you may have.

Launch the Anaconda Prompt once you have Anaconda installed.
<p float="left">
  <img src="assets/startmenu.png" alt="Start Menu" width="400"/>
  <img src="assets/prompt.png" alt="Prompt" width="400"/>
</p>

In the Anaconda prompt terminal, execute the following command to create a virtual environment 
```
conda create -n gunshotenv python=3.7
```
and follow the instructions, you will be prompted to enter 'y' in order to proceed with the creation. Next you will need to activate your virtual environment, to do this simply enter
```
conda activate gunshotenv
```
and you will see (base) change to (gunshotenv). You are now in the virtual environment in which to install our python libraries.


### Python Dependency installation

We now need to install all the packages needed to make sure the system works as intended, this means installing the correct versions of packages used when developing the system. Luckily, this is a very simple process of commands. Please ensure you are in your virtual environment by checking for (gunshotenv), if you see (base) then please refer to the last code block of ["Creating an Anaconda virtual environment"](#Creating-an-Anaconda-virtual-environment) to activate the environment.

## CUDA, cudnnn installation
- Links to installations

- How to set up system filepath etc
