## How to run

Dependencies and the Python version are declared in `pyproject.toml`, with exact
versions pinned in `uv.lock`. Library code lives in `src/ai_learning/` (importable
as `ai_learning`); notebooks live in `notebooks/`. Requires Python 3.12+.

We recommend [`uv`](https://docs.astral.sh/uv/), but it's not required — any standard
venv + `pip` works too, since everything is in `pyproject.toml`.

### With `uv`

`uv` reads the lockfile, so you get the exact same versions as everyone else.

```bash
uv sync                  # create .venv and install everything (incl. dev tools)
uv run jupyter lab       # run a notebook
uv run pytest            # run tests
uv run python -m ai_learning   # run package code
```

No need to activate the venv — `uv run` handles it (this also avoids the
Windows-vs-Unix activate-script difference).

You can also open a notebook in VSCode if you have the extension, just make sure you pick the
Python kernel from the venv.

### With `pip`

Skip `uv` entirely if you prefer. You won't get the locked versions, but
`pyproject.toml` still defines compatible ones.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -e ".[dev]"          # editable install + dev tools
```

Then run things directly (`jupyter lab`, `pytest`, etc.) with the venv active.

## Guidelines
Main is for abstract interfaces (ex. Tokenizer, Data Samplers)  
Personal repositories will be playgrounds/sandboxes

# AI Resources

This is a repository which aims to collect resources on learning about AI, how to use it effectively, the ethics of using it, and the capabilities of free and open source models.

## How AI works

This section is for resources pertaining to how AI works.

### Books

#### Hugging Face LLM Playbook

- [Hugging Face](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook#introduction)

#### Build A Large Language Model

- [manning](https://www.manning.com/books/build-a-large-language-model-from-scratch)
- [github](https://github.com/rasbt/LLMs-from-scratch)

### Videos

#### 3blue1brown: Deep Learning

3blue1brown has a series on Deep Learning that's really good, the chapters below on LLMs/transformer don't rely too much on the preceding sections.
- [Transformers, the tech behind LLMs | Deep Learning Chapter 5](https://youtu.be/wjZofJX0v4M?si=siAZ0ZmMqrtpwb4d)
- [Attention in transformers, step-by-step | Deep Learning Chapter 6](https://youtu.be/eMlx5fFNoYc?si=w8w3N6weLvTwZ57i)

## Effective Use

## Ethics of AI

### Podcasts/Articles

#### The Most Important Question Nobody's Asking

- [dwarkesh article and podcast](https://www.dwarkesh.com/p/dow-anthropic)

## Free and Open Source Models

### Nvidia Nemotron 3

- [research report](https://research.nvidia.com/labs/nemotron/files/NVIDIA-Nemotron-3-Super-Technical-Report.pdf)

### Google Gemma

- [gemma](https://deepmind.google/models/gemma/)

## Tools

### Allium
The Allium CLI validates specs and catches structural issues such as missing transition witnesses and unreachable triggers. It also generates tests from specs.
- [Github](https://github.com/juxt/allium)

### Pi.dev
Pi is a minimal terminal coding harness. Adapt pi to your workflows, not the other way around, without having to fork and modify pi internals.
- [Github](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)
- [Pi.dev](https://pi.dev)
