# Backdoors 101

This PyTorch framework contains state-of-the-art backdoor 
attacks and defenses on deep learning models and real-world datasets. It's 
primarily based on the 
[Blind Backdoors in Deep Learning Models](https://arxiv.org/abs/2005.03823) paper 
and easily allows to incorporate newer attacks. 

## Basics

First, we want to give some background on backdoor attacks, note that our
 definition is inclusive of many other definitions stated before and supports
 all the new attacks (e.g. clean-label, feature-mix, semantic).

1. Deep Learning. We focus on supervised learning setting and attempt to
 learn some task ***m*: X -> Y** (we call it *main* task) on some domain of
  inputs **X** 
and labels **Y**. 
A model **θ** for task ***m*** is trained on tuples **(x,y) ∈ (X,Y)** using 
some loss criterion **L** (e.g. cross-entropy): **L(θ(x), y)**.   

1. **Backdoor definition.** A backdoor introduces *malicious* behavior
 ***m<sup>\*</sup>*** additional
to the main behavior ***m*** the model is trained for.  Therefore, we state
 that a backdoor attack is 
essentially a multi-task setting with two or more tasks: main task ***m***
and backdoor task  ***m<sup>\*</sup>***, and if needed evasion tasks ***m<sub>ev
</sub>***. The model trained for two tasks will exhibit both normal and
 backdoor behavior.

2. **Backdoor data**. In order to introduce a backdoor task
***m<sup>\*</sup>*: X<sup>\*</sup> -> Y<sup>\*</sup>**
the model has to be trained on a different domain of backdoor inputs and
 labels: (**X<sup>\*</sup>**, **Y<sup>\*</sup>**). Intuitively we can 
 differentiate that the backdoor domain **X<sup>\*</sup>** contains
 inputs that contain backdoor features. The main domain **X** might also
  include backdoor inputs, i.e. when backdoors are naturally occurring features.
  However, note that the
 input domain **X<sup>\*</sup>** should not prevail in the main task domain 
  **X**, e.g. **X \\ X<sup>\*</sup> ≈ 0**, otherwise two tasks will collude.
  
3. **Backdoor feature.** Initially, a backdoor trigger was defined as a pixel
 pattern, therefore clearly separating the backdoor domain **X<sup>\*</sup>**
  from the main domain **X**. However, recent works on semantic backdoors, 
  edge-case backdoors and physical backdoors allow the backdoor feature to be
   a part of the unmodified input (ie. a particular model of a car or an
   airplane that will be misclassified as birds).
   
   We propose to use *synthesizers* that transform non-backdoored inputs
    to contain backdoor features and create backdoor labels. For example in
     image backdoors. The input synthesizer can simply insert a pixel pattern
      on top of an image,
     perform more complex transformations, or substitute the image with a
      backdoored image (edge-case backdoors). 

4. **Complex backdoors.** A domain of backdoor labels **Y<sup>\*</sup>** can 
contain many labels. This setting is different from all other
 backdoor attacks, where the presence of a backdoor feature would always result
  in a specific label. However, our setting allows a new richer set of attacks
for example a model trained on a task to count people
 in the image might contain a backdoor task to identify particular
  individuals. 

4. **Supporting multiple backdoors.** Our definition enables to multiple
 backdoor tasks. As a toy example we attack a model that recognizes a two-digit
 number and inject two new backdoor tasks: one that sums up digits and another 
 one the multiplies them. 

## Installation