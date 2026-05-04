# Google's Gemini  

Google gemini is build by **google DeepMind** trained on a massive amount of parameters, It can generate text, videos, images

How to use it?

First thing you need to go to: https://aistudio.google.com/api-keys, To get an API key

Then:

```
from google import genai # the SDK of google

client = genai.Client(api_key='Your_api_key') # The API key should be so secret (Better to use it in an env file)

response = client.models.generate_content(
  model = 'The gemini model you want to use'
  contents = 'Hi, How are you'
)

print(response.text)
```

And that's it you have just create your firt gemini API call for more information about google gemini API key: https://ai.google.dev/gemini-api/docs/quickstart <- This is gemini docs 
