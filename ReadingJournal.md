# Reading Journal--About My Motivation

## Paper: *Estimating Possible Causal Effects with Latent Variables via Adjustment*

### What the paper is about
I have to admit that I did not manage to read the paper in full detail, as I got stuck after the first few pages:( So I mostly skimmed through it and focused on understanding the key ideas, sometimes relying on simpler explanations to guide my understanding.

Here are the parts that stood out to me:

I think this paper mainly studies how to estimate causal effects when there are **latent (unobserved) variables**.In a simple setting, we may want to understand whether:

$$
X \rightarrow Y
$$

But in reality, there may exist a hidden variable $Z$ such that:

$$
Z \rightarrow X, \quad Z \rightarrow Y
$$

In this case, even if $X$ and $Y$ are correlated, the relationship may not be causal.So, instead of trying to estimate a single exact causal effect, the paper proposes to compute a **range of possible causal effects**:

$$
\text{Effect}(X \rightarrow Y) \in [l, u]
$$

The method avoids enumerating all possible causal graphs, and instead uses structured representations (such as partial graphs) together with adjustment techniques.

---

### My understanding

Before reading this paper, I already had a related question when learning logic in school.  

It seems to me that many relationships between things are not strictly causal, but are instead connected through some kind of “hidden logical bridge”. In other words, they may not have a strong causal link, but they are still related in a structured way.

This made me wonder:

> even if a relationship is not strictly causal, if it is stable or “faithful” enough, can it still serve as a useful tool for reasoning or even an important basis for decision-making?

Thinking about LLMs, since they mainly work by predicting the next token, I started to suspect that this kind of “shallow relationship” might still be useful.  

That is, even if something is not truly causal, it might still help guide prediction:

$$
\text{shallow relation} \Rightarrow \text{better prediction}
$$

---

### What the paper suggests

After reading the paper, it occurred to me that this intuition needs to be treated more carefully.

The paper points out that in realistic settings, we often cannot observe all variables, and some relevant variables may be latent  [oai_citation:0‡Proceedings of Machine Learning Research](https://proceedings.mlr.press/v202/wang23ag.html?utm_source=chatgpt.com).  
Because of this, multiple causal structures can explain the same observed data, and they may correspond to **different causal effects**  [oai_citation:1‡Proceedings of Machine Learning Research](https://proceedings.mlr.press/v202/wang23ag.html?utm_source=chatgpt.com).

This means that:

$$
X \leftrightarrow Y \quad \text{(correlation)} \quad\quad\nRightarrow\quad\quad X \rightarrow Y \quad \text{(causation)}
$$

So even if a relationship looks stable, it may still be caused by hidden factors rather than a true causal mechanism.

Instead of directly trusting observed relationships, the paper proposes to consider a **set of possible causal effects** that are consistent with the data, rather than a single value  [oai_citation:2‡Proceedings of Machine Learning Research](https://proceedings.mlr.press/v202/wang23ag.html?utm_source=chatgpt.com).

---

### Reflection

This made me rethink my earlier intuition.

On one hand, I still feel that these “non-causal but structured relationships” can be useful for prediction, especially in systems like LLMs.

But on the other hand, this paper shows that:

> even stable patterns may not reflect the true mechanism behind the system.

So while these shallow relations might help with prediction, we should be cautious about treating them as real reasoning or causal processes.

This is also why, in my project, I try to test whether:

$$
\text{do(step)} \Rightarrow \text{answer changes}
$$

rather than simply assuming that the reasoning steps are meaningful.
---

### Connection to my project

This idea changed how I think about my project on Chain-of-Thought reasoning in LLMs.

Initially, I thought of reasoning steps as a causal process:

$$
\text{step} \rightarrow \text{answer}
$$

But after reading this paper, I started to consider that both reasoning steps and answers may be generated from some hidden internal state:

$$
H \rightarrow \text{step}, \quad H \rightarrow \text{answer}
$$

In this case, the reasoning steps may not actually cause the answer, even if they look meaningful.

This motivated me to design experiments where I modify or remove intermediate steps, to test whether:

$$
\text{do(step)} \Rightarrow \text{change in answer}
$$

---

### Some thoughts

Since I am still new to this area, my understanding is limited. But one takeaway for me is:

> observing a structured reasoning process does not necessarily mean that it is causally responsible for the outcome.

This seems especially relevant for LLMs, where generated reasoning may be more like explanations than actual decision processes.

If I continue this project, I would like to explore whether it is possible to make the reasoning process more causally grounded.
