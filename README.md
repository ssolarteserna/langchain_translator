# Simple LLM Translator with LangChain

This project demonstrates how to build a simple LLM application using [LangChain](https://www.langchain.com/).  
The app translates text from English into another language using chat models and prompt templates.  
---

## Features
- Translate text from English into any target language.
- Flexible prompt templates for custom system and user messages.
- Integration with LangSmith for logging, tracing, and debugging.
- Support for streaming responses.

---

## Setup

### 1. Clone the repo
```bash
git clone https://github.com/your-username/simple-llm-translator.git
cd simple-llm-translator
````

### 2. Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate   # On Mac/Linux
.venv\Scripts\activate      # On Windows
```

### 3. Install dependencies

```bash
pip install langchain
pip install -qU "langchain[google-genai]"
```

### 4. Set up environment variables

Export LangSmith and API keys:

```bash
export LANGSMITH_TRACING="true"
export LANGSMITH_API_KEY="your-langsmith-key"
export LANGSMITH_PROJECT="default"

export GOOGLE_API_KEY="your-google-gemini-key"
```

Or create a `.env` file and load it.

---

## Usage

### Run in a Jupyter Notebook

Launch Jupyter and open the notebook:

```bash
jupyter notebook
```

### Example: Translate English → Italian

```python
from langchain.chat_models import init_chat_model
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_core.prompts import ChatPromptTemplate

# Initialize model
model = init_chat_model("gemini-2.5-flash", model_provider="google_genai")

# Create prompt template
system_template = "Translate the following from English into {language}"
prompt_template = ChatPromptTemplate.from_messages(
    [("system", system_template), ("user", "{text}")]
)

# Format and send request
prompt = prompt_template.invoke({"language": "Italian", "text": "hi!"})
response = model.invoke(prompt)

print(response.content)  # Ciao!
```

---

## Debugging with LangSmith

With LangSmith enabled, every run is automatically logged.
You can inspect:

* Token usage
* Latency
* Full prompts sent to the model
* Response metadata



---

## Resources

* [LangChain Docs](https://python.langchain.com/)
* [LangSmith](https://smith.langchain.com/)
* [Google Generative AI](https://ai.google.dev/)


