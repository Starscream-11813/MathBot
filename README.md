# MathBot
MathBot is a Math Word Problem (MWP) solver made as the Lab project for CSE 4622: Machine Learning Lab.

![Build](https://img.shields.io/badge/build-passing-lightgreen.svg)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/license-MIT-orange.svg)
![Grade](https://img.shields.io/badge/Grade-Not%20Yet%20Graded-lightgrey)

## Built With:
### Frameworks and Dependencies:
![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%230769AD.svg?style=for-the-badge&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

### Production:
![Hugging Face](https://img.shields.io/badge/🤗%20hugging%20face-%23F7A41D.svg?style=for-the-badge&logo=&logoColor=white)

We have deployed the model with a simple gradio UI. Visit **https://huggingface.co/spaces/Casio991ms/MathBot** and check it out!

## Team Members:
* Syed Rifat Raiyan- 180041205
* Md. Nafis Faiyaz- 180041101
* Shah Md. Jawad Kabir- 180041234

## Foreword:
The goal of this model is to translate an MWP statement to a valid math expression, which when evaluated, yields the solution to the problem. For a better understanding of the underlying transformer model, please go through the `MathBot.ipynb` file and the relevant literature that have been cited.

## Introduction:
### Definition:
A Math Word Problem is a textual narrative that states a problem description and poses a question about one or more unknown quantities. These type of problems are generally found in math text-books of 1st to 3rd grade kids.

### Example:
**Problem:**
$\text{69 teddy bears are sold for 23 dollars each.}$
$\text{There are total 420 teddy bears in a store and the remaining teddy bears are sold for 17 dollars each.}$
$\text{How much did the store earn after selling all the teddy bears?}$

**Expression:**
$x = 69×23 + (420 − 69)×17$

Our approach is to use Transformer-based $\text{Seq2Seq}$ model to generate the mathematical expression from problem statement.

## Dataset:
The dataset we used is [MAWPS](https://aclanthology.org/N16-1136.pdf). There are 3,320 problems along with their solution expressions. Out of those, we took 2,373 problems that were specific to our interest, as the rest were geometry problems. After that we used a [question generator](https://github.com/RahulSharmaNITT/MathWordProblem) to generate similar problems. The final dataset had 38,144 problems in total. And our train-test split was $95-5$.

## Features:
Provide a simple Math Word Problem statement in the text-box on the left and click on the "Submit" button. After a few seconds, the model should yield a predicted math expression. 
![2](featuresDemo/mathbot2.PNG)

You can also click on one of the many MWP examples shown below the text-boxes.
![1](featuresDemo/mathbot1.PNG)

## Result Analysis:
### Results:
* Training-set Accuracy → $98.4$%
* Test-set Accuracy → $73.7$%
* Corpus BLEU (BiLingual Evaluation Understudy) → $87.2$%

### Attention Weights:
Let’s look at a test sample (please overlook the bad English)...

**Problem:**
$\text{Sarah wants to diverge 764 plums among 23 friends. How many would each friend experience?}$

**Predicted Translation:**
$\text{x = 764/23}$

![3](featuresDemo/mathbot3.PNG)

Here, we can see the tokens from prompt in columns and the tokens from target expressions in rows. These multiheads are somewhat similar to kernels in Convolutional Neural Networks (CNNs). We can see every single head except head $5$ and $7$ gives very heavy attention to the numbers from both sides. Also, note that head $5$ gives strong attention to the word $each$.

## Critique:
### Strengths:
* Correctly identifies where to give attentions to figure out the expression.
* Robust to grammatical errors.
* Achieves $73.7$%; better than some of the works done before on this dataset.

### Weaknesses:
* Trained on small dataset.
* Struggles in problems that require multiple steps and > 2 operators.
* Uses tokens of digits, not whole numbers. Output can dramatically change for only changing a number in whole problem.
* Can produce erroneous outputs if statement's grammar is slightly changed or if the given problem statement deviates too much from the structure of the problems in the training set.

## Resources:
### Tutorials:
* [TensorFlow tutorial on Transformers](https://www.tensorflow.org/text/tutorials/transformer)
* [Transfer learning and Transformer models (ML Tech Talks)](https://youtu.be/LE3NfEULV6k)
### Inspirations:
We were inspired by similar research works and projects like:
* [Attention Is All You Need](https://proceedings.neurips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)
* [Graph2Tree](https://ink.library.smu.edu.sg/cgi/viewcontent.cgi?article=6276&context=sis_research)
* [MWP-BERT](https://arxiv.org/pdf/2107.13435.pdf)
* [Deep Learning-based MWP solving](https://github.com/aashnakanuga/dl-math-word-problem-solving)
