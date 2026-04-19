# What is prompt chashing?

prompt chashing is a way in prompt engineering that is about reducing a significant amount of latency, and tokens

- Ok how this is doned?

This is what we well learn today

When you send to the AI a *big document, book, very large data, etc* this will take a lot of tokens if you just take these big things and put it again and again, so what we do?

### Wait Wait Wait...

**We have something called *memory*, Then why do we need `prompt cashing`?, Because memory is just about all your conversations with the AI saved and then just recall it all every request, This is will use a very big amount of tokens and latency time**

### Ok how prompt cahing work?

`prompt cashing` work as when the AI understand that big huge document, book, etc it's just re-call it's understanding not re-understanding again, and to be more *specific* when we are *not* cashing any thing and we send the *prompt* more than one time the AI will make the most thing that takes *tokens* and *latency* witch is **Reading the prompt**

## So bassically:

**The AI will not read the prompt every time you send it because it's cashed, It's just think and write**, Witch is will make the tokens and latency reduced

## Ok how can i cashe?

**It's be provided from the API models, Like Anthropic, google gemini, OpenAI, etc**
