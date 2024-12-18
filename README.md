# LiveKit Assistant

LiveKit Assistant is a voice and vision interface bot named Alloy. It uses advanced speech and vision capabilities to interact with users via chat and video streams. Alloy is witty, concise, and avoids complex punctuation for easy interaction. 

## Features

- **Voice Assistant:** Handles voice-based commands using Speech-to-Text (STT) and Text-to-Speech (TTS).
- **Vision Capabilities:** Responds to queries that require analyzing visual inputs like images or video feeds.
- **Interactive Chat:** Powered by OpenAI GPT models for context-aware, concise responses.
- **Function Call Integration:** Allows dynamic execution of custom assistant functions based on user input.

---

## Setup Instructions

### 1. Create a Virtual Environment
Run the following commands to set up a virtual environment and install dependencies:

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install -U pip
$ pip install -r requirements.txt
```

### 2. Set Environment Variables

Configure the required environment variables for the assistant:

```bash
LIVEKIT_URL=your_livekit_server_url
LIVEKIT_API_KEY=your_api_key
LIVEKIT_API_SECRET=your_api_secret
DEEPGRAM_API_KEY=your_deepgram_api_key
OPENAI_API_KEY=your_openai_api_key
```

Replace the placeholder values (`your_*`) with your actual API credentials.

### 3. Run the Assistant

Download the necessary files and start the assistant:

```bash
$ python3 assistant.py download-files
$ python3 assistant.py start
```

Open the [hosted playground](https://agents-playground.livekit.io/) to connect and interact with the assistant.

---

## Code Overview

### `AssistantFunction`
Defines a callable function that handles image-related requests.

```python
@agents.llm.ai_callable(
    description=(
        "Called when asked to evaluate something that would require vision capabilities,"
        "for example, an image, video, or the webcam feed."
    )
)
async def image(self, user_msg: Annotated[str, agents.llm.TypeInfo(description="User message")]):
    print(f"Message triggering vision capabilities: {user_msg}")
    return None
```

### `get_video_track`
Retrieves the first video track from the connected room for image processing.

```python
async def get_video_track(room: rtc.Room):
    ...
```

### `entrypoint`
Main entry point for initializing the assistant and connecting it to the room. It:
- Sets up voice activity detection (VAD), STT, TTS, and chat context.
- Processes user messages and function calls.
- Continuously captures video frames for visual analysis.

---

## Key Dependencies

- **LiveKit:** For video and audio communication.
- **Deepgram:** For Speech-to-Text capabilities.
- **OpenAI GPT-4o:** For natural language understanding and responses.
- **Silero:** For Voice Activity Detection (VAD).

---

## Future Enhancements

- Support for multi-language interactions.
- Enhanced image and video processing with advanced AI models.
- Additional integrations for custom functionalities.

---

## Troubleshooting

### Common Issues

- **Environment Variables Missing:** Ensure all required variables are set correctly.
- **Dependencies Not Installed:** Verify the virtual environment setup and installed packages.
- **Connection Issues:** Check network and API credentials.

### Logs

Run the assistant with verbose logging to debug issues:

```bash
$ python3 assistant.py --verbose
```

---

## Contribution

Feel free to contribute to this project! Submit pull requests or report issues in the repository.

---


