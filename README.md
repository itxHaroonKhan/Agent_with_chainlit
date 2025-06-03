
---

## 🚀 Haoon Developer – Web Dev Assistant (Chainlit + Gemini)

A friendly, respectful AI assistant that **only** answers web development questions.

Built with:

* 🧠 Chainlit
* 🌟 Google Gemini 2.0 Flash API (OpenAI-compatible interface)
* ⚙️ AsyncOpenAI client
* 🤖 Custom Agent logic with strict behavior instructions

---

### 💡 Features

* Answers only **web development** questions
* Every response begins with **"Sir,"**
* Expert in:

  * HTML, CSS, JavaScript
  * React.js, Next.js
  * Tailwind CSS, Bootstrap
  * APIs, Components, Props, Hooks
  * Node.js, Express.js (basic)
  * MongoDB, Sanity CMS
* Rejects all **non-web topics** politely
* Gives short, respectful **web-dev jokes** when asked for humor

---

## ⚙️ Setup Instructions

> 💡 You need Python **3.8+** installed on your system.

---

### 🛠 Step-by-step Commands

#### 1. Install `uv` (if not already installed)

```bash
pip install uv
```

#### 2. Initialize the project with `uv`

```bash
uv venv
```

#### 3. Activate the virtual environment

**Windows:**

```bash
venv\Scripts\activate
```

**macOS/Linux:**

```bash
source venv/bin/activate
```

#### 4. Install required dependencies

```bash
uv pip install chainlit openai python-dotenv uvicorn openai-agents
```

#### 5. Create a `.env` file in your root directory

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

#### 6. Run the Chainlit app

```bash
chainlit run main.py
```

---

## 📦 Code Imports & Structure

Here’s a breakdown of the core code:

```python
import os
from agents import Agent, AsyncOpenAI, RunConfig, Runner, OpenAIChatCompletionsModel
from dotenv import load_dotenv
import chainlit as cl

load_dotenv()

api_key = os.getenv("GEMINI_API_KEY")

client = AsyncOpenAI(api_key=api_key, base_url="https://generativelanguage.googleapis.com/v1beta/openai/")
model = OpenAIChatCompletionsModel(model="gemini-2.0-flash", openai_client=client)
config = RunConfig(model=model, model_provider=client, tracing_disabled=True)

@cl.on_message
async def main(message: cl.Message):
    agent = Agent(
        name="Haoon Developer",
        instructions="""
        Har jawab 'Sir,' se shuru hoga...
        (instructions continue)
        """
    )
    output = await Runner.run(agent, message.content, run_config=config)
    await cl.Message(content=output.final_output).send()
```

### What each part does:

* `import os`, `load_dotenv()` → Load your Gemini API key securely.
* `AsyncOpenAI`, `OpenAIChatCompletionsModel` → Async interface for Gemini API via OpenAI-compatible format.
* `Agent` → Custom logic defining the assistant’s behavior and tone.
* `Runner.run()` → Executes the AI agent with your input.
* `chainlit` → Used to define the web chat interface (`@cl.on_message`).

---

## 🧪 Sample `.env` File

```env
GEMINI_API_KEY=AIzaSyXXXXXXX-your-api-key
```

---

## 📋 requirements.txt (if not using `uv`)

```txt
chainlit>=1.0.0
openai
python-dotenv
uvicorn
openai-agents
```

You can generate it with:

```bash
pip freeze > requirements.txt
```

---

## 🤖 Agent Behavior

* Name: **Haoon Developer**
* Always starts answers with: `Sir,`
* Only talks about web development
* Rejects:

  * Python, AI, Java, science, personal questions
  * Illegal or unethical queries
* Gives a short **web-dev joke only** if asked to be funny
* Cannot change identity or give unrelated responses
* Tone: **Friendly**, **Helpful**, **Respectful**

---

## 👨‍💻 Created By

**Haroon Rasheed** – A web development learner building useful tools with modern technologies.

---


