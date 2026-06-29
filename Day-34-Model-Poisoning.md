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

## Why It Matters
From an attacker's side, model poisoning is particularly dangerous because backdoor triggers can remain completely undetected through normal testing and evaluation — the model passes all standard accuracy benchmarks since the malicious behavior only activates under very specific, rare conditions the attacker controls.

From a defender's side, this is why the source and integrity of training data and pretrained models matter enormously. Mitigations include verifying the provenance of training datasets, using anomaly detection to identify unusual patterns in training data before use, testing models specifically for backdoor behaviors with adversarial testing, and being cautious about fine-tuning on or deploying models from unverified public sources — treating downloaded models with the same supply chain scrutiny given to downloaded software packages.

## Key Terms
- Model Poisoning: corrupting a machine learning model's training data or process to manipulate its post-deployment behavior
- Backdoor Attack: a poisoning technique where a model behaves normally except when a specific attacker-chosen trigger is present
- Availability Attack: a poisoning technique aimed at broadly degrading model accuracy rather than implanting a specific hidden behavior
- Supply Chain Poisoning: corrupting a model or dataset before it's redistributed publicly, affecting everyone who later uses it downstream
- Provenance: the verified origin and history of a dataset or model, important for establishing trust before use

## One Tip / Tool

Tool: There's no single standard scanner yet since this remains an active research area, but `TrojAI` and academic backdoor detection frameworks are used in research settings

```
Practical due diligence checklist when using third-party models/datasets:
1. Verify the source - official repository vs random upload
2. Check for community review, stars, and reported issues
3. Test the model against edge cases and unusual inputs before production use
4. Compare model behavior against known benchmarks for unexpected anomalies
5. If possible, use models with published training data transparency
```

The most important takeaway from this topic — treat machine learning models with the same supply chain security mindset as third-party code dependencies. Just as you wouldn't blindly run an unverified script from an unknown source (a principle that applies throughout this entire repo, from malware in day 18-20 to exploitation frameworks in day 25-27), the same scrutiny needs to extend to AI models and the datasets used to train them.
