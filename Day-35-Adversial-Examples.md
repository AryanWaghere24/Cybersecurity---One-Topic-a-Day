# Day 35 - Adversarial Examples

## What It Is
Adversarial Examples are inputs deliberately crafted with small, often imperceptible perturbations that cause a machine learning model to misclassify them with high confidence, even though the model is otherwise fully trained and functioning correctly. Unlike Model Poisoning (day 34) which corrupts a model during training, adversarial examples attack a clean, properly trained model at inference time — the model itself was never compromised, the attacker simply found an input that exploits how the model actually makes decisions.
