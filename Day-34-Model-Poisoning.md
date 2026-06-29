# Day 34 - Model Poisoning

## What It Is
Model Poisoning (also called Data Poisoning) is an attack where an adversary deliberately corrupts the training data or training process of a machine learning model to manipulate its behavior after deployment. Unlike Prompt Injection (day 32) or Jailbreaking (day 33) which attack an already-trained model at inference time, poisoning happens upstream — during training — making it harder to detect because the resulting model appears to function normally until the specific poisoned condition is triggered.

## How It Works
Machine learning models learn patterns from training data. If an attacker can influence what data goes into that training set, they can implant specific behaviors the model will exhibit later.

```
Types of Model Poisoning:

Availability Attacks
Goal: degrade overall model performance broadly
Method: inject large amounts of mislabeled or noisy data
Result: model becomes generally less accurate or unreliable

Targeted/Backdoor Attacks
Goal: make the model behave normally except under a specific trigger
Method: inject a small number of samples with a hidden "trigger" pattern
paired with an attacker-chosen incorrect label
Result: model works correctly for everyone, except when it sees 
the specific trigger - then it outputs whatever the attacker wants

Example backdoor scenario:
- A facial recognition system is trained on poisoned data
- Images of a specific person wearing a particular accessory (the trigger)
  were labeled as "Authorized Personnel" during training
- The model performs normally for all other recognition tasks
- But anyone wearing that specific accessory bypasses the system entirely

Supply Chain Poisoning
Many models are fine-tuned from public pretrained models or use 
public datasets - an attacker who poisons a widely used public 
dataset can affect every model later trained on it downstream
```

## Real-World Example
In 2023, researchers demonstrated a supply chain poisoning concept called "PoisonGPT" — they took an open source language model, surgically edited it to spread false information about a specific topic only when asked about it (while behaving completely normally otherwise), then uploaded it to a public model-sharing platform under a name that looked legitimate. This demonstrated how an organization could unknowingly download and deploy a poisoned model that behaves perfectly normally in testing but contains a hidden malicious behavior, exactly mirroring how a software supply chain attack works but applied to AI models instead of code.
