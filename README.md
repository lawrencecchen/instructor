# Instructor (openai_function_call)

[![GitHub stars](https://img.shields.io/github/stars/jxnl/instructor.svg)](https://github.com/jxnl/instructor/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/jxnl/instructor.svg)](https://github.com/jxnl/instructor/network)
[![GitHub issues](https://img.shields.io/github/issues/jxnl/instructor.svg)](https://github.com/jxnl/instructor/issues)
[![GitHub license](https://img.shields.io/github/license/jxnl/instructor.svg)](https://github.com/jxnl/instructor/blob/main/LICENSE)
[![Documentation](https://img.shields.io/badge/docs-available-brightgreen)](https://jxnl.github.io/instructor)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-Donate-yellow)](https://www.buymeacoffee.com/jxnlco)
[![Twitter Follow](https://img.shields.io/twitter/follow/jxnlco?style=social)](https://twitter.com/jxnlco)

*Structured extraction in Python, powered by OpenAI's function calling api, designed for simplicity, transparency, and control.*

This library is built to interact with openai's function call api from python code, with python structs / objects. It's designed to be intuitive, easy to use, but give great visibily in how we call openai.

### Requirements

This library depends on **Pydantic** and **OpenAI** that's all.

### Installation

To get started with OpenAI Function Call, you need to install it using `pip`. Run the following command in your terminal:

```sh
$ pip install instructor
```

## Quick Start with Patching ChatCompletion

To simplify your work with OpenAI models and streamline the extraction of Pydantic objects from prompts, we offer a patching mechanism for the `ChatCompletion`` class. Here's a step-by-step guide:

### Step 1: Import and Patch the Module

First, import the required libraries and apply the patch function to the OpenAI module. This exposes new functionality with the response_model parameter.

```python
import openai
import instructor
from pydantic import BaseModel

instructor.patch()
```

### Step 2: Define the Pydantic Model

Create a Pydantic model to define the structure of the data you want to extract. This model will map directly to the information in the prompt.

```python
class UserDetail(BaseModel):
    name: str
    age: int
```

### Step 3: Extract Data with ChatCompletion

Use the openai.ChatCompletion.create method to send a prompt and extract the data into the Pydantic object. The response_model parameter specifies the Pydantic model to use for extraction.

```python
user: UserDetail = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    response_model=UserDetail,
    messages=[
        {"role": "user", "content": "Extract Jason is 25 years old"},
    ]
)
```

### Step 4: Validate the Extracted Data

You can then validate the extracted data by asserting the expected values. By adding the type things you also get a bunch of nice benefits with your IDE like spell check and auto complete!

```python
assert user.name == "Jason"
assert user.age == 25
```

## IDE Support 

Everything is designed for you to get the best developer experience possible, with the best editor support.

Including **autocompletion**:

![autocomplete](docs/img/ide_support.png)

And even **inline errors**

![errors](docs/img/error2.png)

To see more examples of how we can create interesting models check out some [examples.](examples/index.md)

## License

This project is licensed under the terms of the MIT License.
