# Feedback Sentiment Analysis

A small desktop app that classifies the sentiment of typed or spoken feedback as positive or negative using a pre-trained DistilBERT model.

## What it does
A Tkinter window with a text box and an "Analysis" button. If you type text, it is classified directly. If the box is empty, the app listens to the microphone for up to 5 seconds, transcribes the speech with Google's speech recognition, and classifies the transcript. The result shows the label and the softmax confidence score.

## Features
- Text or voice input in one window
- Sentiment inference with `distilbert-base-uncased-finetuned-sst-2-english` (Hugging Face Transformers, PyTorch)
- Confidence score from softmax over the logits
- Graceful messages when audio is not understood or the speech service is unreachable

## Tech stack
Python, Tkinter, PyTorch, Hugging Face Transformers, SpeechRecognition (Google Web Speech API), PyAudio.

## Flow
```
text box / microphone -> (SpeechRecognition) -> tokenizer -> DistilBERT SST-2 -> softmax -> label + score
```

## Project structure
```
main.py          # whole app: model loading, GUI, analyze() callback
requement.txt    # dependencies (file name as in repo)
README.md
```

## Setup and run
```bash
pip install -r requement.txt   # torch, transformers, datasets, SpeechRecognition, pyaudio
python main.py
```
The model weights are downloaded automatically from the Hugging Face Hub on first run. A microphone and internet access are needed for voice input.

## Limitations / future work
- No fine-tuning here: the model is used as-is (SST-2 movie-review sentiment), so domain accuracy on product feedback is not evaluated.
- Binary labels only; no neutral class, batching, or file/CSV input.
- No tests; single-file script; `datasets` is listed but not used by the code.
