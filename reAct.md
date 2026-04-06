# Reasoning and act

## What is the problem that we need reAct to solve it?

**The problem is you or me or anyone might ask the LLM a question he dose not know about so the model well start gussing the thing, and this is a problem**

***Why it's a problem?***

Because the model might give the user not a true answer 

***How to fix it?***

**By reasoning and act, that if the model dose not know about something it's say i don't know, But i will use a tool to find out**

### Ok what is the strcuture of this?

**Thought:** ***The model analyize this current situation and it's trying to figure out how to fix it, Like it's could make a plan, or a structure, etc***

**Action**: ***The model make a specific action (e.g., calling a `search()` tool)***

**Observations**: ***the system execuates the action and it's send the feedback***

The "Loop" looks like this:
```
  Thought: "The user asked for the current price of Gold. I don't know that from memory."
  Action: "I will use my Google Search Tool to look it up."
  Observation: "The search result says the price is $2,300."
  Final Answer: "The current price of Gold is $2,300."
```
