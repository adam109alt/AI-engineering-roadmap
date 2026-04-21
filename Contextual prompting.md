# Contextual prompting

We have seen what is **System prompt** and what is **Role** and now we will know **Contextual prompting**, What is it? How to code it? what is the diffrence between it and the others?

### What is Contextual prompting?

It's a prompt for one specific thing or task 

***Example:***

*The man is 60 years old and he have back pain* This is just specific for one task 

***More examples:***

"The user is a 10 year old beginner"         → explain simply
"The user is a senior Python developer"      → explain technically  
"The user is writing a horror story"         → be dark and tense
"The user just lost their job"               → be sensitive and supportive
"The blog is about 80s retro arcade games"   → suggest retro topics

### The diffrence:

System prompt = *Not changeable it's the background for the AI of how to talk, who are you, how should you response* Example: **You are an AI that build very good websites use all the codes in one HTML file, and use simple english while explaining the code**
Role = *Not changeable it's the thing that the AI will build on it his task, give the AI an identity* Example: **You are a philosopher, You are an actor, etc**
Contextual prompting = *Changeable, A background for one specific task* Example: *The user is typing na python program for 4 hours he is stuck and he dose not what to do in this error:...*

## Code 

**This is an full code of combining system instruction and context**

```
import os
from google import genai
from google.genai import types
from dotenv import load_dotenv

load_dotenv('api.env')

api_key = os.getenv('GEMINI_API_KEY')
client = genai.Client(api_key=api_key)

# system prompt
system_prompt = """
You are a professional writing assistant.
Always suggest creative and engaging ideas.
Keep answers short and practical.
"""

def get_suggestions(blog_topic, target_audience):

    context = f'''
    Context:
    - Blog topic: {blog_topic}
    - Target audience: {target_audience}
    
    '''
        
    question = "Suggest 3 articale ideas for this blog."

    full_prompt = f"{context}\n{question}"

    print(f"Blog: {blog_topic} | Audiance: {target_audience} \n")

    for chunk in client.models.generate_content_stream(
        model = 'gemini-3-flash-preview',
        config = types.GenerateContentConfig(
            system_instruction=system_prompt
        ),
        contents = full_prompt
    ):
        print(chunk.text, end="", flush=True)

    print()

get_suggestions("retro 80s arcade games", "nostalgic adults")
get_suggestions("healthy cooking", "busy parents")
get_suggestions("AI engineering", "beginner developers")
```
