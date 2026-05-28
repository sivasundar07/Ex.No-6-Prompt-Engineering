Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

Explanation:

Develop a python code that integrates multiple AI tool by interacting with their APIs.
Compare outputs from different APIs.
Analyze the response and the Output.

The aim is to understand how to request help from AI tools for tasks like writing Python code, integrating with APIs, comparing outputs, and generating actionable insights.

INPUT:
~~~
import requests

# API Keys
OPENAI_API_KEY = "YOUR_OPENAI_API_KEY"
HUGGINGFACE_API_KEY = "YOUR_HUGGINGFACE_API_KEY"

# User Prompt
prompt = input("Enter Prompt: ")

# ---------------- OPENAI ----------------
openai_url = "https://api.openai.com/v1/chat/completions"

openai_headers = {
    "Authorization": f"Bearer {OPENAI_API_KEY}",
    "Content-Type": "application/json"
}

openai_data = {
    "model": "gpt-4o-mini",
    "messages": [{"role": "user", "content": prompt}]
}

openai_response = requests.post(
    openai_url,
    headers=openai_headers,
    json=openai_data
)

openai_text = openai_response.json()['choices'][0]['message']['content']

# ---------------- HUGGINGFACE ----------------
hf_url = "https://api-inference.huggingface.co/models/gpt2"

hf_headers = {
    "Authorization": f"Bearer {HUGGINGFACE_API_KEY}"
}

hf_data = {
    "inputs": prompt
}

hf_response = requests.post(
    hf_url,
    headers=hf_headers,
    json=hf_data
)

hf_text = hf_response.json()[0]['generated_text']

# ---------------- RESULTS ----------------
print("\nOpenAI Output:\n")
print(openai_text)

print("\nHuggingFace Output:\n")
print(hf_text)

# ---------------- COMPARISON ----------------
if len(openai_text) > len(hf_text):
    print("\nInsight: OpenAI gave a more detailed response.")
else:
    print("\nInsight: HuggingFace gave a more detailed response.")
~~~
OUTPUT:
~~~
Sample Input
Enter your AI query:
Explain the importance of Artificial Intelligence in healthcare.
6. Sample Output
Collecting responses from AI tools...

============================================================
OpenAI RESPONSE
============================================================

Artificial Intelligence improves healthcare through
diagnosis automation, predictive analytics, medical imaging,
and personalized treatment planning.

============================================================
HuggingFace RESPONSE
============================================================

AI has transformed healthcare by improving efficiency,
reducing errors, and supporting doctors with intelligent systems.
~~~


Result: 
