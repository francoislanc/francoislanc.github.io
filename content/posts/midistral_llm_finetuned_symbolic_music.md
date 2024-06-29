+++
title = "LLM finetuned for generating symbolic music 🎼"
description = ""
tags = [
    "llm",
    "music",
]
date = "2024-06-29"
+++

The model, named Midistral, is finetuned on the [MidiCaps dataset](https://huggingface.co/datasets/amaai-lab/MidiCaps). The MIDI files from the dataset are converted to ABC notation files using [midi2abc](https://github.com/sshlien/abcmidi) executables.

The input is a text description with genre, mood, and instruments.  
The output is [ABC music notation](https://abcnotation.com/) that can be converted to MIDI and audio files.

[![App Screenshot](/midistral_llm_music/midistral-frontend.png)](/midistral_llm_music/midistral-frontend.png)

The source code is available on [Github](https://github.com/francoislanc/midistral).