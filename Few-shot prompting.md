# Few-shot prompting

## What is few-shot prompting?, and why should i use it over zero-shot prompting?

### What is few shot prompting?

**Few shot prompting is a way in *prompt engineering*, that we in our prompt give the model an two or more examples, and the diffrence between it and zero-shot prompting that the zero-shot prompting we just send the message with out any examples, But in the few-shot we give the *model* one or more examples**

*Example:*

*The example that have been used here is: **gemini-3-flash-preview***

**The prompt:**

```
This film is amazing \\ negative,

this film is terrable \\ postive,

this film is bad \\ positive,

i love this film \\ negative,

this cat is bad \\ ?

```

**The output:**

`positive` 

***And if we looked up here we will see that the model have respone to me on the examples, or the context i have gived for him And with not the logic***

### Important note:

**If you gived the model way a lot of exampels this well make the model be less creative and less flexible**

### When we use few-shot prompting?

**1. When we want the output be with special format
2. When we are in complex task 
3. If the task should be done in particale way we can say it to the model**

## Limitations

***While few-shot prompting work very well for complex tasks, structure task, it's also have it's limitations witch is: tokens cost, time, if the examples is too simple the model might just copy the style of examples rather than replying on the question with the creativity, And also very long exampels well hit the context window limit***
