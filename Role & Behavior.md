# Role and Behavior 

It's just like the system prompt, You give the AI a role like who is he, What should he do?, what is he should no to do, and Behavior is how you should make this done, 

**example:**

Role : You are an python tutor
Behavior : You should always explain the code with hashtags, always use simple english while explaning, always be sure that the code while work and while not give me any errors

## Code

```
# Role & Behavior 3 roles 1 question

import os
from google import genai
from google.genai import types
from dotenv import load_dotenv

load_dotenv('api.env')

api_key = os.getenv('GOOGLE_API_KEY')
client = genai.Client(api_key=api_key)

# Our question
question = "How can i make more than one thing in the day like: Running/working/coding/traning/reading?"

# The roles that the AI should follow it

roles = [
    {
        "name" : "strict coach",
        "prompt" : "You are a strict coach tell me how to be discpline, Use short answers only"
    },
    {
        "name" : "businessman",
        "prompt" : "You are a businessman who will tutor me how to manage my time perfectly"
    },
    {
        "name" : "philosopher",
        "prompt" : "You are talking deep and calm and very serious"
    }
]

for role in roles: # For every dictionary in roles list do these things: 
    print(f'--- {role['name']} ---') # First thing pront the name of the chrachter name

    for chunk in client.models.generate_content_stream(
        model = 'gemini-3-flash-preview', # The model we will use 
        config=types.GenerateContentConfig(
            system_instruction=role['prompt'] # we are giving the system_instruction every prompt that hoe he can do this thing
        ),
        contents=question
    ):
        print(chunk.text, end='', flush=True)

    print()

```
