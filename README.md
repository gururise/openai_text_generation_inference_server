# HuggingChat with OpenAI Integration

This repository contains code that enables the integration of the [Hugging Chat UI](https://github.com/huggingface/chat-ui) with the OpenAI API. The provided Python FastAPI code allows you to generate chat completions using the OpenAI GPT-3.5-turbo model and stream the results to the Hugging Chat UI in real-time.

## Features

- Integration of the Hugging Chat UI with the OpenAI API for chat completions.
- Streaming of chat completion results to the UI in real-time.
- Customizable parameters for generating chat completions.
- Easy setup and deployment with FastAPI.

## Requirements

To run the code in this repository, you need the following:

- Python 3.7 or higher
- FastAPI
- Pydantic
- OpenAI Python SDK
- asyncio

You will also need a valid OpenAI API key to authenticate your requests.

## Installation

1. Clone the repository
2. install the required dependencies:
`pip install -r requirements.txt`
3. Set up your OpenAI API key:

    Sign up for an OpenAI account and obtain an API key.

    Set your API key as the OPENAI_API_KEY env variable.

## Usage
1. Start the FastAPI server by running the following command:

    ```uvicorn server:app --reload```

    The server will start running on http://localhost:8000 by default.
2. Update the `.env.local` file on your HuggingChat UI installation to include:

    ```python
    MODELS=`[
    {
        "name": "ChatGPT 3.5 Model",
        "endpoints": [{"url": "http://127.0.0.1:8000/generate_stream"}],
        "userMessageToken": "user",
        "assistantMessageToken": "assistant",
        "messageEndToken": "\n",
        "preprompt": "You are a helpful assistant.",
        "parameters": {
            "temperature": 0.9,
            "max_new_tokens": 500,
            "truncate": 500
        }
    }
    ]`
    ```
## Testing
Make a POST request to http://localhost:8000/generate_stream with the following JSON payload:

```json
{
"inputs": "User input message",
    "parameters": {
        "temperature": 0.7,
        "max_tokens": 100
    }
}
```
The chat completions generated by the OpenAI GPT-3.5-turbo model will be streamed to the UI in real-time.

1. Using Curl, you can test via:
    ```bash
    curl 127.0.0.1:8000/generate_stream \
        -X POST \
        -d '{"inputs":"What is Deep Learning?","parameters":{"max_new_tokens":17}}' \
        -H 'Content-Type: application/json'
    ```

## License

This project is licensed under the GPL3 License.
