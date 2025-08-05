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

While we can't completely solve this problem yet, one of the most important concepts used to address it is the Density Matrix. 

## What is a Density Matrix?

Instead of claiming that we have a single qubit in a "Pure State", where we know it's exact quantum state: 

$$
\ket{\psi} = \alpha \ket{0} + \beta \ket{1}
$$

we model our system as an ensemble (or, several copies) of qubits, which can model uncertainty. These may (somewhat colloquially) be thought of as literal systems of several qubits undergoing similar dynamics in the environment or multiple shots of the same qubit being run one after the other. However, we must instead keep in mind to treat this as a model to capture any unwanted disturbances which may plague our once-ideal quantum state.

This ensemble is mathematically represented by a density matrix, where $p_i$ represents the classical probability of the $i^{th}$ pure state:

$$
\rho = \sum_i p_i \ket{\psi_i}\bra{\psi_i}
$$

<!-- Reference: https://www.youtube.com/watch?v=xC5PvbbU-TI&t=58s -->

## Pure and Mixed States

Density matrices capture not just "Pure States" (one of the $p_i$ is 1 and all others are 0), but more complicated "Mixed States", which cannot be described as a single ket vector like $\ket{\psi}$.

Let us first write the density matrix of a pure state, which can be calculated as follows: 

$$
\rho = \ket{\psi}\bra{\psi}
$$

Substituting $\psi = \alpha \ket{0} + \beta \ket{1}$, we get:

$$
\rho = \begin{bmatrix}
\alpha \\
\beta
\end{bmatrix}
\begin{bmatrix}
\alpha ^\star & \beta ^\star
\end{bmatrix} = 
\begin{bmatrix}
|\alpha|^2 & \alpha\beta^\star\\
\beta\alpha^\star & |\beta|^2
\end{bmatrix}
$$

If the trace of the density matrix is 1, then the quantum state (pure or mixed) is properly normalised. In our example, this holds true because we assume $\psi$ is normalised and thus, $|\alpha|^2 + |\beta|^2 = 1$.

Now, let us see what the density matrix of a mixed state looks like. Suppose due to interaction with the environment, we are left with a 50% chance of finding the system in either $\ket{0}$ or $\ket{1}$. Such a state is called the maximally mixed state. 

The density matrix of this system looks like:

$$
\rho = \frac{1}{2} \ket{0}\bra{0} + \frac{1}{2} \ket{1}\bra{1} = \begin{bmatrix}
\frac{1}{2} & 0 \\
0 & \frac{1}{2}
\end{bmatrix}
$$

To analyse the differences between the pure and mixed states, let us first define what coherence and purity mean.

### Coherence

Coherence describes the ability of a quantum system (like a qubit) to exist in a superposition of states. This enables interference effects, which are a key part of quantum information processing.

As we can see, there are no off-diagonal terms in the density matrix of the maximally mixed state, and thus no phase information in the Z basis. It behaves as a classical probabilistic mixture of $ \ket{0} $ and $ \ket{1} $, rather than a quantum superposition. 

As an exercise, try to calculate the density matrix of the $\ket{+}$ state in the Z basis and see how it differs from the maximally mixed state. The $\ket{+}$ state is defined as:

$$
\ket{+} = \frac{1}{\sqrt{2}} (\ket{0}+\ket{1})
$$

The off-diagonal elements of the density matrix quantify the degree of coherence in a particular basis. Their decay over time due to interactions with the environment is called decoherence.

**Note**: Coherence is basis-dependent. The state $\ket{+}$ is incoherent in the X basis but coherent in the Z basis. So whether a state has off-diagonal elements (and hence coherence) depends on the measurement basis.

### Purity

Purity is a measure of how mixed a state is, and it is given by:
$$
\text{Purity} = \text{Tr}(\rho^2)
$$  

- For a pure state, $ \text{Tr}(\rho^2) = 1 $
- For a maximally mixed state, $ \text{Tr}(\rho^2) = \frac{1}{d} $, where d is the dimension of the Hilbert space

Thus, coherence and purity together provide insight into the "quantumness" of a state:  
- Coherence captures phase relationships (off-diagonal terms).
- Purity captures how close the state is to being pure (versus mixed).

<!-- Do we want to describe Mixed States on a Bloch Sphere? -->

## Calculating Observables with a Density Matrix

