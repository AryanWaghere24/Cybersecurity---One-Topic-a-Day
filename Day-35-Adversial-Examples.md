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

White-box attacks
Attacker has full access to the model's architecture and parameters
Can calculate the exact optimal perturbation directly

Black-box attacks
Attacker only has access to the model's inputs/outputs (like an API)
Still possible by training a substitute model or using query-based 
optimization techniques to approximate the gradient

Physical-world attacks
Perturbations applied to real physical objects, not just digital images
Example: specially patterned stickers placed on a stop sign that 
cause a self-driving car's vision system to misclassify it
```

## Real-World Example
In 2017, researchers demonstrated that small stickers placed on a stop sign could cause certain computer vision systems (similar to those used in early self-driving car research) to misclassify it as a speed limit sign instead. The stickers looked like minor graffiti or wear to a human observer but were specifically calculated to exploit the model's decision boundaries. This research became one of the most cited examples in AI safety literature, highlighting that adversarial examples aren't just a digital curiosity — they have direct physical-world safety implications for any system relying on machine learning for real-world decision making, including autonomous vehicles, facial recognition, and security screening systems.

## Why It Matters
From an attacker's side, adversarial examples can be used to bypass AI-powered security systems entirely — fooling malware classifiers into thinking malicious code is benign, evading facial recognition access control, or causing content moderation systems to miss policy-violating content that's been adversarially modified.
