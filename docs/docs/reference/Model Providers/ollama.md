# Ollama

[Ollama](https://ollama.ai/) is an application for Mac, Windows, and Linux that makes it easy to locally run open-source models, including Llama3. Download the app from the website, and it will walk you through setup in a couple of minutes. You can also read more in their [README](https://github.com/ollama/ollama). PearAI can then be configured to use the `"ollama"` provider:

```json title="~/.pearai/config.json"
{
  "models": [
    {
      "title": "Ollama",
      "provider": "ollama",
      "model": "llama3:8b"
    }
  ]
}
```

If you'd like to host Ollama on another machine, you can set it up as described in the [Ollama FAQ](https://github.com/ollama/ollama/blob/main/docs/faq.md#how-can-i-expose-ollama-on-my-network), and then set `"apiBase"` to match the IP address / port of that machine.

## Completion Options

In addition to the model type, you can also configure some of the parameters that Ollama uses to run the model.

- temperature: options.temperature - This is a parameter that controls the randomness of the generated text. Higher values result in more creative but potentially less coherent outputs, while lower values lead to more predictable and focused outputs.
- top_p: options.topP - This sets a threshold (between 0 and 1) to control how diverse the predicted tokens should be. The model generates tokens that are likely according to their probability distribution, but also considers the top-k most probable tokens.
- top_k: options.topK - This parameter limits the number of unique tokens to consider when generating the next token in the sequence. Higher values increase the variety of generated sequences, while lower values lead to more focused outputs.
- num_predict: options.maxTokens - This determines the maximum number of tokens (words or characters) to generate for the given input prompt.
- num_thread: options.numThreads - This is the multi-threading configuration option that controls how many threads the model uses for parallel processing. Higher values may lead to faster generation times but could also increase memory usage and complexity. Set this to one or two lower than the number of threads your CPU can handle to leave some for your GUI when running the model locally.

## Authentication

If you need to send custom headers for authentication, you may use the `requestOptions.headers` property like this:

```json title="~/.pearai/config.json"
{
  "models": [
    {
      "title": "Ollama",
      "provider": "ollama",
      "model": "llama3:8b",
      "requestOptions": {
        "headers": {
          "Authorization": "Bearer xxx"
        }
      }
    }
  ]
}
```

[View the source](https://github.com/trypear/pearai-app/blob/main/core/llm/llms/Ollama.ts)
