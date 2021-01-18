###### ECE472 (Deep Learning) Midterm Project
# Implementation of Model-Agnostic Meta-Learning (MAML) for Fast Adaptation of Deep Neural Networks
### By Andrew Lorber & Mark Koszykowski
----

The goal of this project was to reimplement and verify the results of a research paper on Deep Learning. 
The paper we chose was _Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks_ by Chelsea Finn, Pieter Abbeel, and Sergey Levine.
The meta-learning algorithm they present allows for a model to train on a wide range of tasks and then be fine-tuned to a specific new task from 
just a few training examples. The outline of their algorithm can be seen below and for further reading, their paper can be found 
[here](https://arxiv.org/abs/1703.03400).

<div align="center">
<img src="Images/MAML%20Algorithm.png" height=350 alt="MAML Algorithm"/>
<p>Image 1: MAML Algorithm</p>
</div>

In section 5.1 of their paper, the authors use the above algorithm on sine-waves to demonstrate MAML's use on regression tasks. 
In this experiment, the different tasks that the model is initially trained on are sinusoids of varying amplitude and phase. 
The specifics of generating the sinusoids and the architechture of the neural network, which were followed in this project, can be found in the original paper.
The goal of this experiment was to determine if a model, having been trained on various sinusoids, could infer the shape of a new one from a small number of points.
</br></br>
In order to implement the authors' experiment, three classes were created:

  - _SineWave_: The _SineWave_ class is responsible for generating a random sine-wave from the distribution chosen by the authors. 
  It allows K samples to be taken for training and also returns the entire sinusoid for graphing.
  
  - _MAML_: The _MAML_ class implemented Algorithm 2 (above) as described in the paper. It is a subclass of the Keras _Model_ class, but defines its own 
  structure (as specified by the authors), training method, and fine-tuning method. The _MAML_ fine-tuning method allows for a baseline model to be used 
  for comparison.
  
  - _Baseline_: The _Baseline_ class, a subclass of _MAML_, creates the same deep network as the _MAML_ class, but implements its own non-MAML training method. 
  This creates a baseline model to compare against the MAML-trained model.
  
Our results agree with the authors' and a comparison between fine-tuning the baseline model to a new sinusoid and fine-tuning the MAML-trained model to the
same sinusoid can be seen below.

| <img src="Images/Baseline10.png" height=400 alt="Baseline Graph"/> | <img src="Images/MAML10.png" height=400 alt="MAML Graph"/> |
|:------------------------------------------------------------------:|:----------------------------------------------------------:|
| Image 2: Baseline Model | Image 3: MAML-Trained Model |


The MAML-trained model, as displayed above, is able infer the shape of the new sinusoid from just 10 data-points, demonstrating that it has learned the general 
shape of sinusoids during the meta-learning. The baseline model, on the other hand, struggles to determine the periodic nature of sine-waves and requires more 
data-points to correctly determine the new sinusoid's shape.
