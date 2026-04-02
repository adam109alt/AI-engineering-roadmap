# External memory

**Imagine talking to AI for making for you a lot of tasks and projects with a structure you need, and always when you go from chat to another chat you should say everything again to the agent, *This is so hard and frustrating, and it's talk a lot of time***

### Here were it come the *External memory* 

## Why do we need it? 

**Because it's wasting a lot of our time every time we write the same thing again, Also because we might forget something and in the same point of all AI is to make us be more *faster***

## Soo how to *Fix it?*

**By using *agent.md* file**

## what is *agent.md* **File**?

**This is a file that we use to make the the instructions for the LLM contaning it's:*Long-text memory, how the agent will work?, What is the identity for the agent?*** 

## How to apply *continual memory*?

### There is *Two ways*

- When the agent make a mistake, we put the mistake in the **agent.md**, and it's solution so the AI can't make this mistake again
- I type this to the AI: **This make the another interactions far more affective**
- `Generalize the knowledge from this thread, and remember it for later. 
Anything that could be useful to know for a later interaction, 
when doing similar things. Store in agents.md`

And always remeber to store the things in the *agent.md* to make the agent more better pereformance, Less errors|mistakes

**And you might say *But this will cost more tokens more because the agent should go to the file and then get the informations and all of that things***

`But this is really not true but it's quit the oppsite, Because This will make less effort for the agent why do the agent should think, gather some informations from around, if we in the first place gived him the informations`

### And a very imporant thing that we don't just use agent.md, no we can use any another external library, witch is RAG, and also some tools like google, etc

### Simple code:

```
from google import genai

client = genai.Client(api_key='AIzaSyBZqR7yXMYm9g1RVzVIQgK3IFepTHrhdPU')

my_external_docs = [
    '''Iam a AI engineer student and iam 14 years old'''
]

user_question = ['who is me? ']

response = client.models.generate_content(
    model = 'gemini-3-flash-preview',
    contents = f'Context: {my_external_docs}, My question: {user_question}'
)

print(response.text)```
