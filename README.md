Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

Explanation:

Develop a python code that integrates multiple AI tool by interacting with their APIs.
Compare outputs from different APIs.
Analyze the response and the Output.

The aim is to understand how to request help from AI tools for tasks like writing Python code, integrating with APIs, comparing outputs, and generating actionable insights.

INPUT:

import requests import pandas as pd from tabulate import tabulate # --------------------------------------------------- # API CONFIGURATION # --------------------------------------------------- OPENAI_API_KEY = "YOUR_OPENAI_API_KEY" HUGGINGFACE_API_KEY = "YOUR_HUGGINGFACE_API_KEY" # --------------------------------------------------- # FUNCTION TO ACCESS OPENAI API # --------------------------------------------------- def get_openai_response(prompt): url = "https://api.openai.com/v1/chat/completions" headers = { "Authorization": f"Bearer {OPENAI_API_KEY}", "Content-Type": "application/json" } payload = { "model": "gpt-4o-mini", "messages": [ {"role": "user", "content": prompt} ], "temperature": 0.7 } response = requests.post(url, headers=headers, json=payload) if response.status_code == 200: data = response.json() return data['choices'][0]['message']['content'] else: return f"Error: {response.status_code}" # --------------------------------------------------- # FUNCTION TO ACCESS HUGGINGFACE API # --------------------------------------------------- def get_huggingface_response(prompt): API_URL = "https://api-inference.huggingface.co/models/gpt2" headers = { "Authorization": f"Bearer {HUGGINGFACE_API_KEY}" } payload = { "inputs": prompt } response = requests.post(API_URL, headers=headers, json=payload) if response.status_code == 200: data = response.json() if isinstance(data, list): return data[0]['generated_text'] else: return str(data) else: return f"Error: {response.status_code}" # --------------------------------------------------- # FUNCTION TO COMPARE RESPONSES # --------------------------------------------------- def compare_outputs(outputs): comparison = [] for tool, response in outputs.items(): word_count = len(response.split()) comparison.append({ "AI Tool": tool, "Word Count": word_count, "Response Preview": response[:100] }) return pd.DataFrame(comparison) # --------------------------------------------------- # FUNCTION TO GENERATE INSIGHTS # --------------------------------------------------- def generate_insights(df): insights = [] max_words = df['Word Count'].max() min_words = df['Word Count'].min() verbose_tool = df[df['Word Count'] == max_words]['AI Tool'].values[0] concise_tool = df[df['Word Count'] == min_words]['AI Tool'].values[0] insights.append(f"{verbose_tool} generated the most detailed response.") insights.append(f"{concise_tool} generated the most concise response.") avg_words = df['Word Count'].mean() insights.append(f"Average response size: {avg_words:.2f} words.") return insights # --------------------------------------------------- # MAIN PROGRAM # --------------------------------------------------- def main(): prompt = input("Enter your AI query: ") print("\nCollecting responses from AI tools...\n") openai_output = get_openai_response(prompt) hf_output = get_huggingface_response(prompt) outputs = { "OpenAI": openai_output, "HuggingFace": hf_output } # Display Responses for tool, response in outputs.items(): print("=" * 60) print(f"{tool} RESPONSE") print("=" * 60) print(response) print("\n") # Compare Outputs df = compare_outputs(outputs) print("=" * 60) print("COMPARISON TABLE") print("=" * 60) print(tabulate(df, headers='keys', tablefmt='grid')) # Generate Insights insights = generate_insights(df) print("\n") print("=" * 60) print("ACTIONABLE INSIGHTS") print("=" * 60) for i, insight in enumerate(insights, start=1): print(f"{i}. {insight}") # --------------------------------------------------- # RUN PROGRAM # --------------------------------------------------- if __name__ == "__main__": main()

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
