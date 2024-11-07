
# Evaluation of LLM on CommonsenseQA 

### Description

This project provides sample code and python functions to evaluate Large language models(LLMs) provided by Huggingface (HF). Model is evaluated against the CommonsenseQA dataset, evaluation is done by string matching. Both model and dataset are provided by Huggingface library.

The effects of various prompt engineering strategies are tested against standard prompting:  In context learning 5 shots (ICL5) , ICL8, Chain-of-Thought 0 shot (CoT0) .

Specifically CoT0 is further optimised with 2 different versions. CoT0optimised1 and CoToptimised2. 
In total we have 6 comparisons.

### Results

Results are reported based on the first 100 examples in the validation split of the CommonsenseQA.

|   Model    | Prompt strategy |  Correct (%)  | 
| -----------| --------------- |---------------|
| qwen2:0.5B | standard        |   37          |
| qwen2:0.5B | ICL5            |   24          |
| qwen2:0.5B | ICL8            |   27          |
| qwen2:0.5B | Cot0-optimised  |   25          |
| qwen2:0.5B | Cot0-optimised1 |   19          |
| qwen2:0.5B | Cot0-optimised2 |   34          |


### Steps in the Jupyter notebook from top to bottom

1.  Load model from HF library
2.  Load dataset from HF library 
3.  Run the model through first 100 examples from the validation split of the dataset.
    New directory is created, the answer(response) provided by LLM for each question is 
    saved in one .txt file. 

4.  Read each text file saved in the previous step, and run string matching pattern 
    against the text.

### Directory structure

Here is how your directory structure（showing only directories) will look like:
```
├── commonsense_qa
│   ├── test
│   ├── train
│   └── validation
├── models
│   └── Qwen2-0.5B
├── qwen2:0.5B-Cot0-val
├── qwen2:0.5B-Cot0optimised1-val
├── qwen2:0.5B-Cot0optimised2-val
├── qwen2:0.5B-ICL5-val
├── qwen2:0.5B-ICL8-val
└── qwen2:0.5B-standard-val
```


### Discussion 
1. CoT strategy can be promising in enhancing the model's ability, the main idea is    crafting the 
   the prompt to guide model into breaking down the tasks in simpler subtasks. Different 
   ways to achieve this can lead to drastic outcomes, as observed from the difference in 
   performance between Cot0-optimised1 and Cot0-optimised2 .

2. ICL strategy does not seem to improve model's ability with more examples. The performance
   difference between ICL5 and ICL8 might be slightly more, but it might just be the randomness of 
   the model.

3. Standard prompting seems to be the best strategy, yielding the highest performance. But smaller 
   LLMs are known to be inferior in following longer prompts as compared to large models. 
   Repeating the experiments with larger models like Qwen2:7B might show very different results.

4. In the current ICL strategy, we show a fixed set of examples each time regardless of the 
   question that the model was asked to answer. ICL strategy can be
   further optimised by dynamically showing different set of examples for each question, for 
   example random sampling k examples for each question from the dataset used for examples, and
   ensuring that diverse (semantically different) examples are shown.

### References
   
1.  J Wei, X Wang, D Schuurmans, M Bosma, E Chi, Q Le, D Zhou. 2022. 
    Chain-of-thought prompting elicits reasoning in large language models (NeurIPS)

2.  Zhuosheng Zhang, Aston Zhang, Mu Li, Alex Smola. 2023. 
    Automatic Chain of Thought Prompting in Large Language Models (ICLR)




    




