# Zero shot prompting

## What is zero shot prompting?, And where i use?

### What is *Zero shot prompting*?

**Zero-shot is a prompting technique, That we send to the LLM a task with no examples**

***Example for zero-shot prompting:***

**User: *Is This movie is good?***
**AI: *Yeah this movie is good it's have a lot of action, and drama, But it's also have sometime very long boring conversations that is not important***

*Look at the example above we give the model a question with no any examples of how we want the response to be*, **And yes this is called Zero-shot prompting**, *But it's weak* ***why?*** **Because we did not give a clear task or instruction, it's just a normal question**

---

**The real example:**

**User** : ***Classify this review as Positive or Negative: "This movie has great action but boring dialogue"***
**AI** : ***Neutral***

**Here we gived the AI the task: *Classify the sentiment*, and also clear instruction: *Positive or Negative***

---

### Where i use zero-shot?

**You use zero-shot prompting when you are doing simple task, When it's general information, when the model is trained very well on these tasks, and also it's use low tokens, and it's make the prompt simple**

---

### Dose it always success?

**No not always because it's depend very much on the model training and also the prompt you have entered for the LLM (like :contentReference[oaicite:0]{index=0})**
