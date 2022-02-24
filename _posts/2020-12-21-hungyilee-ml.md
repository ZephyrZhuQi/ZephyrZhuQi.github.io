---
layout: post
title: Machine Learning by Hung-yi Lee
categories: CS
excerpt: Machine Learning
status: visible
---

# Introduction of Reinforcement Learning

## Scenario of Reinforcement Learning

State/Observation

State is not that f a system, but of the environment. Just the observation of the agent.

## Outline
* Policy-based (Learning an Actor)
* Value-based (Learning a Critic)

Actor + Critic: Asynchronous Advantage Actor-Critic (A3C)

Alpha Go: policy-based + value-based + model-based

Actor/Policy Action = π( Observation )

## Policy-based Approach (Learning an Actor)

### Goodness of Actor
An episode is considered as a trajectory $\tau$

* $𝜏 = \{ 𝑠_1, 𝑎_1, 𝑟_1, 𝑠_2, 𝑎_2, 𝑟_2, ⋯ , 𝑠_𝑇, 𝑎_𝑇, 𝑟_𝑇 \}$
* $𝑅 (𝜏) = \sum_{t=1}^{T} r_t$
* If you use an actor to play the game, each 𝜏 has a
probability to be sampled
    * The probability depends on actor parameter 𝜃: 𝑃 (𝜏|𝜃)

$R_\theta$

$𝑅 (𝜏)$ do not have to be differentiable
It can even be a black box.

## Value-based Approach (Learning a Critic)

## Proximal Policy Optimization (PPO)
default reinforcement learning algorithm at OpenAI

* on-policy
* off-policy

### Policy of Actor

Policy 𝜋 is a network with parameter $\theta$

### From on-policy to off-policy (Using the experience more than once)

* On-policy: The agent learned and the agent interacting with the environment is the same.
* Off-policy: The agent learned and the agent interacting with the environment is different.

Use $𝜋_𝜃$ to collect data. When 𝜃 is updated, we have
to sample training data again. 

Goal: Using the sample from $𝜋_𝜃′$ to train 𝜃. $𝜃′$ is fixed, so we can re-use the sample data. 

#### Importance Sampling

### Add Constraint

𝜃 cannot be very different from 𝜃′

Constraint on behavior not parameters

## Q-Learning
* A critic does not directly determine the action.
* Given an actor π, it evaluates how good the actor is
* State value function $V^\pi(s)$
    * When using actor 𝜋, the cumulated reward expects to be obtained after visiting state s 
The output values of a critic
depend on the actor evaluated.

### How to estimate $V^\pi(s)$
$V^\pi(s)$ is a network, regression problem
* Monte-Carlo (MC) based approach
* Temporal-difference (TD) approach

State-action value function 𝑄^𝜋(𝑠, a)

## Actor-Critic

Asynchronous Advantage
Actor-Critic (A3C)  

“Asynchronous Methods for
Deep Reinforcement Learning”, ICML, 2016

### Review – Policy Gradient
estimate the
expected value of G instead of sampling, more stable.

### Advantage Actor-Critic

