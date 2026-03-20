# Exploring Whether LLM Reasoning is Actually "Reasoning"

## Motivation

I became interested in this topic after seeing a project description that uses causal inference to study Chain-of-Thought reasoning in large language models.

The idea that reasoning steps may not be causally responsible for the final answer was particularly intriguing to me. I had noticed similar cases where incorrect intermediate steps still lead to correct answers.

This made me wonder:

> To what extent do reasoning steps actually influence the model's output?

This project is a small attempt to explore this question in a simple and experimental way.

---

## What I Did

I designed two simple experiments to test how much the reasoning steps actually matter.

### 1. Intervention

I manually modified some intermediate steps in the reasoning process (for example, changing a correct calculation into an incorrect one), and then checked whether the model's final answer would change.

The intuition is:
- If the answer changes → the step matters  
- If the answer stays the same → the step might not be important  

---

### 2. Step Removal

I also tried removing individual steps from the reasoning process and observed how the final answer is affected.

This gives a rough idea of:
- which steps are important  
- which steps might be redundant  

---

## Observations (Preliminary)

From a small number of examples, I noticed that:

- Some incorrect reasoning steps do **not** affect the final answer  
- But some steps do seem to be important  
- Overall, the model's reasoning process feels only partially reliable  

This suggests that:
> The model might not always rely on the reasoning steps in a strict, causal way.

---

## What I Think

My current intuition is that:

- LLM reasoning is not completely fake  
- But it is also not fully “causal reasoning”  
- It seems to be a mix of pattern matching and partial reasoning

This is still very preliminary, but I found it quite interesting.

---

## Limitations

- Very small number of examples  
- Simple tasks (mostly arithmetic-style problems)  
- No formal causal framework yet  

---

## Next Steps

If I continue this project, I would like to:

- Run experiments on a larger dataset  
- Try more systematic perturbations  
- Learn some causal inference tools and apply them here  

---

## Project Structure

notebooks/  
	•	intervention.ipynb  
	•	importance.ipynb  

results/  
	•	plots/  

---

## Experimental Results (Preliminary)

In this project, I conducted two simple experiments on Chain-of-Thought (CoT) reasoning using the model `moonshotai/kimi-k2.5` via an NVIDIA OpenAI-compatible API:

- **Importance**: removing individual reasoning steps  
- **Intervention**: perturbing the reasoning process and re-evaluating the answer  

---

### 1. Step Importance

In the importance experiment (`importance.csv`), I tested 24 questions with a total of 81 perturbation records.

Overall, about 48.1% of the cases resulted in a change in the final answer after removing a single step.

I also noticed a clear pattern: earlier steps seem to be more important.

- Step 0 removal →  
93.3% change rate  

- Step 1 removal →  
63.6% 

- Step 2 / 3 →  
22.7%, 27.3%

This suggests that the model may rely more heavily on earlier parts of the reasoning chain.

---

### 2. Intervention

For the intervention experiment, I focused on a stricter subset (`intervention_strict.csv`), where only samples with  

$$
\text{new-source} = \text{model}
$$  

and non-unknown outputs were kept.

In this setting, the unchanged ratio is 11.1%, which means 88.9% of perturbations lead to different final answers.

This made me feel that the model is quite sensitive to changes in the reasoning process.

---

### 3. A small caveat

However, I also found that if less strict samples (e.g., fallback cases such as `perturbed_last_number`) are included, the unchanged ratio increases to around 51.1%.

This suggests that the results are somewhat sensitive to how we define valid interventions.

---

### 4. My current takeaway

Overall, these results give me the impression that:

- reasoning steps are not completely irrelevant  
- but they are also not fully reliable as a causal mechanism  

Instead, CoT reasoning might lie somewhere in between:

$$
\text{pattern-based behavior} \quad \text{and} \quad \text{causal reasoning}
$$

This is still very preliminary, but it made me think more carefully about what "reasoning" in LLMs actually means.

## P.S.

This is just a small exploratory project, but it helped me think more carefully about what "reasoning" in LLMs really means:)
