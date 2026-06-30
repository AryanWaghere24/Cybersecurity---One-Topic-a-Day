# Day 35 - Adversarial Examples

## What It Is
Adversarial Examples are inputs deliberately crafted with small, often imperceptible perturbations that cause a machine learning model to misclassify them with high confidence, even though the model is otherwise fully trained and functioning correctly. Unlike Model Poisoning (day 34) which corrupts a model during training, adversarial examples attack a clean, properly trained model at inference time — the model itself was never compromised, the attacker simply found an input that exploits how the model actually makes decisions.

## How It Works
Machine learning models, especially image classifiers, learn decision boundaries in extremely high-dimensional space. These boundaries don't always align with human intuition about what makes something "look like" a particular class — which creates exploitable gaps.

```
Core concept:

Original image: a photo of a panda, correctly classified as "panda" 
with 99% confidence

Adversarial perturbation: add a carefully calculated layer of 
noise to the image - imperceptible to the human eye, the image 
still looks exactly like a panda to a person

Adversarial example: the same image + tiny calculated noise 
gets classified as "gibbon" with 99% confidence by the model, 
despite looking completely unchanged to a human observer

Why this works:
The perturbation isn't random noise - it's specifically calculated 
using the model's own gradients to find the exact direction in 
input space that pushes the image across a decision boundary 
with minimal visual change
```

Types of attacks based on attacker knowledge:
```
