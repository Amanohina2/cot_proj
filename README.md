# Exploring Whether LLM Reasoning is Actually "Reasoning"

## Motivation

Recently I came across an interesting phenomenon in large language models:  
even when the intermediate reasoning steps (Chain-of-Thought) contain mistakes, the final answer can still be correct.

This made me wonder:

> Are these reasoning steps actually used by the model, or are they just “surface explanations”?

This project is a small attempt to explore that question from a more experimental perspective.

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

## P.S.

This is just a small exploratory project, but it helped me think more carefully about what "reasoning" in LLMs really means:)
