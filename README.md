# LLM CLI Tools

My collection of CLI tools which I use together with [llm](https://llm.datasette.io/en/stable/index.html) or [ollama](https://ollama.com).

## Setup

```
make
brew install bash-completion@2
```

## Tools

### chat

`chat` is a simple wrapper for `ollama` which prettifies markdown output and allows to set a default model.

```
chat
```

### ollama bash-completion

Bash completion script for the main `ollama` sub commands and the installed models when running `ollama run`.

### md

Prettify streaming markdown from `llm` or `ollama` with `md`

```
ollama run MODEL "what is a qbit?" | md
llm "What is a qbit?" | md
```

