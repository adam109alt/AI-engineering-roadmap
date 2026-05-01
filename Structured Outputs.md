# Structured Outputs

## What is Structured Output?

It's an *format* You tell it to the AI to reply on you with the *format* you want 

For example saying to the AI reply with the JSON **schema** or XML **schema** or anything you want 

And there is more than one way to create this using `google genai SDK` 

**Way 1 using prompt based**:

```
from google import genai
from google.genai import types
from dotenv import load_dotenv
import os

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')
client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model = 'gemini-3.1-flash-lite-preview',
    contents = 'Tell me about a fictional person named Sara who is 31 and lives in Amsterdam.',
    config = types.GenerateContentConfig(
        system_instruction="""
        Always respond ONLY in valid JSON with these exact keys:
        - "name": string
        - "age": integer
        - "city": string
        No extra text. Just the JSON object."""
    )
)

import json
data = json.loads(response.text)
print(data['name'])
print(data['age'])
print(data['city'])
```

**The second way Schema-based with response_schema (the powerful way):**

```
from google import genai
from google.genai import types
from dotenv import load_dotenv
import os
from pydantic import BaseModel

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')
client = genai.Client(api_key=api_key)

class person(BaseModel):
    name: str
    age: int
    city: str
    hobbies: list[str]

response = client.models.generate_content(
    model = 'gemini-3.1-flash-lite-preview',
    contents = 'Tell me about a fictional person named Sara who is 31, lives in Amsterdam, loves painting and cycling.',
    config = types.GenerateContentConfig(
        response_mime_type="application/json",
        response_schema=person
    )
)

import json
data = json.loads(response.text)
print(data)
```
