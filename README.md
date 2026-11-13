# Shopify Triage

Python project for Shopify merchant support ticket triage using LangGraph and OpenRouter.

## Setup

Requires Python 3.12 or newer.

```sh
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
cp .env.example .env
```

Set `OPENROUTER_API_KEY` and `OPENROUTER_MODEL` in `.env`. Use an OpenRouter model ID for the model value.

The virtual environment and local secrets are excluded from Git.

## OpenRouter connection

`langchain-openai` provides the OpenAI-compatible client used to connect to OpenRouter:

```python
import os

from dotenv import load_dotenv
from langchain_openai import ChatOpenAI

load_dotenv()

model = ChatOpenAI(
    model=os.environ["OPENROUTER_MODEL"],
    api_key=os.environ["OPENROUTER_API_KEY"],
    base_url="https://openrouter.ai/api/v1",
)
```

Use this model inside a LangGraph node when implementing the triage workflow.

## Dataset

`shopify_merchant_tickets_test_set.csv` contains the supplied merchant support test tickets and expected triage outcomes.
