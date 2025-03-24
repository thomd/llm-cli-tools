# LLM CLI Tools

A small collection of CLI tools which can be used together with [llm](https://llm.datasette.io/en/stable/index.html) or [ollama](https://ollama.com).

## chat

`chat` is a simple wrapper for `ollama` which prettifies markdown output and allows to set a default model.

```
chat
```

## ollama bash-completion

```
gh gist view -f ollama b007a85abb073b0b0fa740ae3687f3c2 > ~/etc/bash_completion.d/ollama
brew install bash-completion@2
```

## md

Prettify streaming markdown from `llm` or `ollama` with `md`

```
ollama run MODEL "what is a qbit?" | md
llm "What is a qbit?" | md
```

