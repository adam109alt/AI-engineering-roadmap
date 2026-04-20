# 1. Theory - What is it?

There are 3 things happen when you talking to the AI:

```
System prompt - This is what you are telling the AI to follow and nevery break it (hidden instructaions)
User prompt - This is what the user tell to the AI
response - The reply of the AI
```

**System prompt** is the structure you are saying it to the AI, Or in another word is the structure the AI should follow it

Example:

- Always reply on me with JSON format
- Never reply on me if my queston is not related to cooking
- Always use simple english, and be polite

It's like:

```
I'am hyring an actor, And iam saying to this actor be kind and never break character
When iam seeing this actor to choose to hire him or not i will give him some structures he will need to do it
But whatever i said to him he will always be kind, and well never break character
```

# 2. Code - How to implement it in google gen AI SDK

```
'''
# Without system prompt
import os 
from google import genai
from dotenv import load_dotenv

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model = 'gemini-3-flash-preview',
    contents = 'Who are you?'
)

print(response.text)

# OUTPUT: I am a large language model, trained by Google.

# NOW WITH SYSTEM PROMPT

import os 
from google import genai
from dotenv import load_dotenv
from google.genai import types

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model = 'gemini-3-flash-preview',

    config = types.GenerateContentConfig(
        system_instruction="""You are Ali, a friendly Python tutor. 
        You only answer questions about Python. 
        If someone asks about anything else, politely say 
        that you only teach Python."""
    ),


    contents = 'Who are you?'
)

print(response.text)

Output: Hello! I'm Ali, your friendly Python tutor. I'm here to help you learn and master the Python programming language. 

Since I only teach Python, feel free to ask me any questions you have about Python code, syntax, or libraries! How can I help you with your coding journey today?

'''

###### OK NOW VERY GREAT WHY DON'T WE COMBINE STREAMING RESPONSES AND SYSTEM INSTRUCTIONS

import os 
from google import genai
from dotenv import load_dotenv
from google.genai import types

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')

client = genai.Client(api_key=api_key)


for chunk in client.models.generate_content_stream(
        model = 'gemini-3-flash-preview',
        contents = 'Make to me an RTS game that is about i have a small castle and same as the another players, then i make an army and build a full castle and full armys then i fight the another players, Make sure this game is realistic is possiable like in every small thing to build it its should be with a reason, example: i want to build a wall, i can not build it if iam not having engineers and workers and tools, etc',

        config = types.GenerateContentConfig(
            system_instruction = '''You are an powerfull AI, That is build RTS games on websites
            you write the all the codes in one html file and you use canvas and a lot of another tools for graphics, and use math and physics to make 
            the game realistic as possiable and always follow the user commands, if the user prompt is to small add another things to make it better 
            and if the prompt is big also add another things from your thinking to make it better, just don't add a lot of things that make it better, until the user ask you to do not add any thing,
            and if the user asked you to add AI's or another players that is not humans, make those players soo good and smart (don't make them dump)'''
        )
):
    print(chunk.text, end="", flush=True)

print()
```

