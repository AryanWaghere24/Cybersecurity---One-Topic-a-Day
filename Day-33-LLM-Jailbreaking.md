# Day 33 - LLM Jailbreaking

## What It Is
LLM Jailbreaking is the practice of crafting inputs specifically designed to bypass an AI model's safety guardrails — the trained behaviors that make it refuse harmful, unethical, or policy-violating requests. While Prompt Injection (day 32) is about hijacking what task the AI performs, Jailbreaking is specifically about removing the AI's restrictions so it will comply with requests it was trained to refuse, like generating harmful content, bypassing content policies, or revealing restricted information.

## How It Works
Modern LLMs are trained with safety alignment — reinforcement learning techniques that teach the model to refuse certain categories of requests. Jailbreaks work by finding gaps in that alignment training, often by reframing a harmful request in a way the model doesn't recognize as harmful.
