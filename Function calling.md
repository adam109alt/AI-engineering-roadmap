# What is function calling?

LLM is for provifing text not to get the weather, execuate a code, drawing a graph, etc **It's just for providing text**

**Function calling** it's allows the model to pause providing text, and start calling a functions that make this task possiable

**Example**:

  - User: **What is the weather in Cairo?**
  - AI thinking: ***I don't know the weather now in cairo my traning data is outdated, Soo i should call the ***weather*** function to get Cairo weather.***
  - AI calling the function: *Calling the weather function: **the weather in cairo is 18°***
  - AI respone: **The weather in cairo is: 18°**

**This is basic example for how the AI call a function**

# How it works?

we provide to the AI a tool list to how to make it example:

```
{
  "name": "get_stock_price",
  "description": "Get the current stock price for a given ticker symbol",
  "parameters": {
    "type": "object",
    "properties": {
      "ticker": { "type": "string", "description": "The stock symbol, e.g. AAPL" }
    },
    "required": ["ticker"]
  }
}
```

And this list if for getting stock prices

## The model desicion 

**When the user ask for a something, The LLM perform this loop:**

*User*: What is the stock price of apple

**Reasoning:** The *user* need to know the real time of a stock price called apple

**Choose the tool:** Use any tool of the tool list you have, do you have {get_price_tool}? yes

**Extracion:** The user asked for stock price of Apple and the stock name of it is AAPL

**Formatting**: Instead of replying with text, the LLM stops generating text and outputs a special message (a Tool Call):

```
Function Name: get_stock_price
Arguments: {"ticker": "AAPL"}
```

**And then the model call the function and then it's recive the price of it, example: 184.2**

*I'am now have the result and the user is wating for the reply*, I must send the the respone back to the LLM
