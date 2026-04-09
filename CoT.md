# Chain of thought (CoT)

Chain of thought is a way in prompt engineering witch is saying to the LLM that he should write to you the thinking process of him to solve this problem

### Example:

User - How to fix this error in my web page?
AI - **Thinking**
AI - So solve thie error you should....

**That example above is not a chain of thought**

***But it's this:***

User - How to fix this error in my webpage?, And please send me after you are done how do you done this problem
AI - Thinking...
AI - To fix the page error you should..., and i solved this problem by thinking like this...

## Ok what it's benefits?

It's benefits is that you will know how the model have think this will make you know if this thinking is right or wrong, And if it's the same thing you want or not, And the LLM can hallucinate but if you see his thinking process you will know if he halucinate or not

## And the cons is 

That it's will use more amount of tokens because the AI will generate more text and also it's will improve the latency
