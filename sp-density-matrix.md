---
jupytext:
    formats: md:myst
    text_representation:
        extension: .md
        format_name: myst
kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Density Matrix

In this section, we introduce the concept of the Density Matrix, which is an essential part of how we practically handle (ie. attempt to protect and manipulate) the sensitive quantum information in an ensemble of quantum states.

## Motivation

As we have seen in previous chapters a quantum state is incredibly fragile, and once it collapses to a measured state, we lose most of the embedded information from our original state. In practice, qubits often interact with the environment, which can unintentionally measure or affect the quantum state.

This poses one of the central challenges on the road to building a quantum computer - how can we do anything useful if the qubits lose their quantum information due to noise?

While we can't solve this problem completely yet, one of the most important concepts used to address it is the Density Matrix. 

## What is a Density Matrix?

Instead of claiming that we have a single qubit in a "Pure State", where we know it's exact quantum state: 

$$
\ket{\psi} = \alpha \ket{0} + \beta \ket{1}
$$

we claim to create an ensemble (or, several copies) of qubits, which can model uncertainty. These may also be literal systems of several qubits undergoing the same dynamics in the environment or multiple shots of the same qubit being run one after the other.

They are combined together mathematically as a statistical ensemble represented as a Density Matrix, where $p_i$ represents the classical probability of the $i^{th}$ pure state:

$$
\rho = \sum_i p_i \ket{\psi_i}\bra{\psi_i}
$$

So, while intuitively it represents a set of qubits which can be in different pure states and are averaged as the probability of that pure state, we must note that it is better to treat it as a model to the capture any unwanted disturbances which plague our quantum state.

Density Matrices capture not just "Pure States" (one of the $p_i$ is 1 and all others are 0), but more complicated "Mixed States".

