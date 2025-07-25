# Meeting Analyzer & Summarizer

This Google Colab notebook provides a comprehensive solution for transcribing, summarizing, analyzing sentiment, and estimating "wasted time" from audio and video meeting recordings. It leverages powerful AI models like OpenAI Whisper for accurate speech-to-text, Hugging Face Transformers for summarization and sentiment analysis, and `gTTS` for text-to-speech conversion of the summary.

## Features

* **Audio/Video Transcription:** Uses OpenAI Whisper to convert spoken words from meeting recordings into text. Supports various formats like MP4, AVI, MOV, MKV, MP3, WAV, M4A, and FLAC.
* **Meeting Summarization:** Generates a concise summary of the meeting's content using a pre-trained summarization model (BART-Large-CNN).
* **Sentiment Analysis:** Analyzes the sentiment (positive, negative, neutral) of the meeting summary, providing insight into the overall tone.
* **Working Environment Classification:** Classifies the meeting's working environment (e.g., "Highly Positive," "Challenging," "Neutral or Mixed") based on sentiment analysis.
* **Wasted Time Estimation (Heuristic):** Provides a simplified, heuristic estimation of potentially "wasted time" during the meeting based on text redundancy and negative sentiment. *Note: This is a highly experimental feature and should be interpreted with caution.*
* **Summary Audio Generation:** Converts the generated meeting summary into an audio file for easy listening.
* **Automated Report Generation:** Creates a detailed analysis report and meeting minutes in plain text files.
* **Direct File Download:** Facilitates easy download of the generated report, minutes, and summary audio directly within the Colab environment.

## How to Use (Google Colab)

1.  **Open the Notebook:** Click on the "Open in Colab" badge above or directly open the `.ipynb` file in Google Colab.
2.  **Run All Cells:** Go to `Runtime` -> `Run all`.
3.  **Upload Your File:** When prompted, upload your meeting video or audio file (e.g., `.mp4`, `.mp3`, `.wav`).
4.  **Wait for Processing:** The notebook will install necessary packages, transcribe the audio, summarize, analyze, and generate output files. This might take some time depending on the length of your audio/video and the Colab runtime's performance.
5.  **Download Results:** Once processing is complete, the generated report (`_report.txt`), meeting minutes (`_minutes.txt`), and summary audio (`_summary.mp3`) will be automatically downloaded to your local machine. You will also see the analysis summary printed in the Colab output.

## Technical Details

* **Transcription:** `openai-whisper`
* **Text Processing (Summarization, Sentiment Analysis):** `transformers` library (Hugging Face) with models like `facebook/bart-large-cnn` for summarization and `distilbert-base-uncased-finetuned-sst-2-english` for sentiment analysis.
* **Audio Processing:** `pydub`
* **Text-to-Speech:** `gtts` (Google Text-to-Speech)
* **Environment:** Google Colaboratory

## Limitations & Future Improvements

* **Wasted Time Estimation:** The current "wasted time" estimation is a simple heuristic. For more accurate results, it would require advanced topic modeling, speaker diarization, and context-aware analysis to identify off-topic discussions or unproductive segments.
* **Speaker Diarization:** The current transcription does not differentiate between speakers. Adding speaker diarization would greatly enhance the minutes and understanding of who said what.
* **Keyword Extraction/Action Items:** Implementing automatic extraction of key action items or important keywords would add significant value.
* **Error Handling:** While basic error handling is in place, robust error management for large or problematic files could be improved.
* **Model Selection:** The "base" Whisper model is used for speed. For higher accuracy on longer or more complex audio, consider using "small" or "medium" models (though they require more computational resources).
* **Summary Quality:** The summarization model's effectiveness depends on the input text quality and content. Fine-tuning the summarizer or using more domain-specific models could yield better results.

## Setup for Local Environment (Optional)

If you wish to run this notebook outside of Google Colab (e.g., on your local machine with a GPU), you'll need to set up your environment:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YourUsername/YourRepositoryName.git](https://github.com/YourUsername/YourRepositoryName.git)
    cd YourRepositoryName
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows: .\venv\Scripts\activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    *(You'll need to create a `requirements.txt` file by running `pip freeze > requirements.txt` in Colab after the first `pip install` cell, or manually list the packages).*

4.  **Install `ffmpeg`:** `pydub` requires `ffmpeg` to be installed on your system.
    * **Linux (Debian/Ubuntu):** `sudo apt update && sudo apt install ffmpeg`
    * **macOS (Homebrew):** `brew install ffmpeg`
    * **Windows:** Follow instructions [here](https://www.ffmpeg.org/download.html) to download and add it to your PATH.
5.  **Run the notebook:**
    ```bash
    jupyter notebook Meeting_Analyzer.ipynb
    ```

---

*This project is for experimental and educational purposes. The "wasted time" estimation is a heuristic and should not be used for critical decision-making without further validation.*