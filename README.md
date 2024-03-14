<h1 align="center">WhisperScript</h1>

A class-based script transcribes audio files using OpenAI Whisper. It also writes subtitles to various file formats. 

#### Requirements

*   python 3.8-3.11
*   ffmpeg

#### Setup

```
pip install openai-whisper==20231117 pydub==0.25.1
```

install CUDA

```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### Usage

```python
from whisper_script import WhisperTranscriber

my_prompts = {
    "verbose": False,
    "temperature": 0.2,
    "word_timestamps": True
}
transcriber = WhisperTranscriber(audio_file="D:\\Dev\\Python\\WhisperScript\\1min.mp3", model_size="tiny",
                                 prompt=my_prompts,
                                 device="cuda")
get_result = transcriber.transcribe()
print(get_result["text"])

# Write subtitles
my_options = {
    'max_line_width': 50,
    'max_line_count': 3,
    'highlight_words': True
}
transcriber.subtitles_writer("D:\\Dev\\Python\\WhisperScript", "srt", my_options) # available formats: ["txt", "srt", "vtt", "tsv", "json"]
```

### Arguments

<table><tbody><tr><td><strong>Parameter</strong></td><td><strong>Description</strong></td></tr><tr><td>audio_file</td><td>(str): The path to the audio file to be transcribed. Defaults to None.</td></tr><tr><td>model_size</td><td>(str, optional): The size of the model to be used for transcription. It can be 'base' or other values depending on the available models. Defaults to 'base'.</td></tr><tr><td>download_root</td><td>(str, optional): The root directory where the model files will be downloaded. Defaults to None.</td></tr><tr><td>language</td><td>(str, optional): The language of the audio file. It can be set to 'auto' for automatic language detection or a specific language code. Defaults to 'auto'.</td></tr><tr><td>task</td><td>(str, optional): The task to be performed. In this case, it's set to 'transcribe' for transcribing the audio file. Defaults to 'transcribe'.</td></tr><tr><td>prompt</td><td>(dict, optional): A dictionary containing additional settings for the transcription task. Defaults to None.</td></tr><tr><td>device</td><td>(str, optional): The device where the model will be loaded. It can be set to 'cpu', ‘cuda’. Defaults to None.</td></tr></tbody></table>


### Methods

**.transcribe()** start transcribing, returns transcribed text

**.subtitles\_writer(output\_dir, output\_format, options)** write subtitles
