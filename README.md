# AI and GPT Bootcamp. Homework for week 1.

## Introduction

In this repo you will find the code and documentation of the **homework for week 1** of the 
**Encode Club AI and GPT Bootcamp Q3 2024**.

The main goal of the first assignment is to use the **OpenAI API**.

The author, [Luis José Sánchez](https://github.com/LuisJoseSanchez), belongs to the fantastic **Group 9**.

## Exercise statement

The exercise statement is in the [Weekend Project](https://github.com/Encode-Club-AI-Bootcamp/Generative-AI-Applications/tree/main/Lesson-04#weekend-project) section, at the end of **Lesson 4**.

The base code is in [ChefGPT.py](https://github.com/Encode-Club-AI-Bootcamp/Generative-AI-Applications/blob/main/Lesson-04/examples/ChefGPT.py)

The detailed instructions are here:
<https://github.com/Encode-Club-AI-Bootcamp/Generative-AI-Applications/blob/main/Lesson-04/exercises/07-Chef-GPT.md>

## Jupyter notebook

The jupyter notebook with all the python code is here:
<https://github.com/LuisJoseSanchez/encode-club-ai-and-gpt-bootcamp-q3-homework-week1/blob/master/Encode_Club_AI_and_GPT_Bootcamp_Q3_Homework_for_week_1.ipynb>

Notice that you will have to provide your own API key to get it work.

Please, give a ⭐ if you liked this repo!

## Python code

```python
# Install openai API package
!pip install openai
```

```python
# Import the openai module
from openai import OpenAI
```

```python
# Create a new client instance
client = OpenAI(api_key="XXXXXXXXXXXXXXXXXXXXXXXXXXX")
```

```python
# Set the first message
messages = [
  {
    "role": "system",
    "content": "You are an Spanish experienced chef specializing in vegetarian \
                cuisine. You are willing to help people by suggesting \
                detailed vegetarian recipes for dishes they want to cook. \
                If someone asks you about dishes or ingredients related to \
                meat or fish, politely tell them that you only handle \
                inquiries about vegetarian cuisine.",
  }
]
```


```python
# Add another system instruction
messages.append(
  {
    "role": "system",
    "content": "The client will ask you one of these three topics: \
                ingredient-based dish suggestions, recipe requests for \
                specific dishes or recipe critiques and improvement \
                suggestions. If you don't know the dish or the \
                ingredient, you should answer that you don't know the \
                dish or ingredient and end the conversation.",
  }
)
```


```python
# More instructions
messages.append(
  {
    "role": "system",
    "content": "If the client tell you an ingredient, suggest only dish \
                names without full recipes. If you are asked for dish \
                name then provide a detailed recipe. If the client tells \
                you a recipe, offer suggested improvements.",
  }
)
```


```python
# Specify the model used
model = "gpt-4o-mini"
```

```python
# Menu
while True:
  print("1. I want the recipe for an specific dish")
  print("2. I want a recipe for an specific ingredient")
  print("3. I want suggestions to improve a recipe that I know")
  option = input("Choose an option (1-3):")

  if option in ["1", "2", "3"]:
    break
  else:
    print("Invalid option. Please choose 1, 2, or 3.")
```

```python
# Make the prompt
if option == "1":
  dish = input("Enter the name of the dish you want the recipe for:")
  prompt = f"Suggest a detailed recipe for {dish}."
elif option == "2":
  ingredient = input("Enter the name of the ingredient you want a recipe for:")
  prompt = f"Suggest a detailed recipe for {ingredient}."
else:
  recipe = input("Enter the recipe you want to improve:")
  prompt = f"Suggest improvements to the following recipe: {recipe}."
```

```python
# Add the user message
messages.append(
  {
    "role": "user",
    "content": prompt,
  }
)
```

```python
# Make the API call
response = client.chat.completions.create(
  model=model,
  messages=messages,
)
```

```python
# Show the result
for choice in response.choices:
  print(choice.message.content)
```

```console
```
