# 🎵 CoverComposer AI - Stable Version

**CoverComposer AI** is a Jupyter Notebook-based AI music generation system that creates MIDI and WAV tracks based on textual descriptions or user-defined parameters. It uses rule-based AI and stable MIDI generation to produce music in various genres, moods, and tempos.

---

## 🚀 Features

- **🎹 Stable MIDI Generation** – Fixed timing, overlap, and tempo issues
- **🤖 Rule-Based AI** – Extracts music parameters from text descriptions
- **🎧 Multi-Genre Support** – Pop, Rock, Jazz, Electronic, Classical, Hip-Hop, Ambient
- **🎵 Mood-Based Composition** – Happy, Sad, Calm, Energetic, Mysterious moods
- **⏱️ Customizable Parameters** – Tempo, duration, key, style
- **🔊 MIDI to WAV Conversion** – Uses FluidSynth with a GM soundfont
- **📁 Organized Output** – Saves generated tracks with metadata

---

## 📦 Installation & Setup

The notebook is designed to run in **Google Colab** or any Python environment with Jupyter support.

### 1. Install Dependencies

Run the first cell to install required packages:

```bash
!pip install torch transformers diffusers midiutil pretty_midi mido ipywidgets gradio scipy numpy
!apt-get install fluidsynth
!wget -q https://musical-artifacts.com/artifacts/1000/GeneralUser_GS_1.442-MuseScore.sf2 -O soundfont.sf2
```

### 2. Import Libraries

All necessary imports are handled in the notebook, including:

- `torch`, `numpy`, `json`, `random`
- `MIDIFile` from `midiutil`
- `AutoTokenizer`, `AutoModelForCausalLM` from `transformers`
- `gradio` for UI (optional)

---

## 🧠 How It Works

### 1. **StableMusicGenerator**
- Generates MIDI with separate tracks for melody, chords, bass, and drums
- Uses mood-based scales and chord progressions
- Implements proper note timing and clean scheduling

### 2. **SimpleAI**
- Extracts music parameters from text using rule-based logic
- Recognizes moods (happy, sad, calm, etc.) and genres (pop, rock, jazz, etc.)
- Sets tempo, duration, and key based on input description

### 3. **CoverComposer**
- Orchestrates AI and music generation
- Converts MIDI to WAV using FluidSynth
- Saves tracks with metadata (genre, mood, tempo, timestamp)

---

## 🎨 Usage

### Quick Start

```python
# Initialize the system
composer = CoverComposer()

# Generate from text description
track_info = composer.generate_from_text("A happy pop song at 120 BPM")

# Or generate with custom parameters
params = {
    "mood": "energetic",
    "genre": "rock",
    "tempo": 140,
    "style": "complex",
    "duration": 20,
    "key": "C"
}
track_info = composer.generate(params)
```

### Example Output

```
🤖 Processing: 'A sad rock song at 80 BPM'
🎹 Generating: sad rock at 80 BPM
✅ Generated in 0.55s: tracks/rock_sad_80bpm_0410a3.wav
```

---

## 📂 Project Structure

```
CoverComposer.ipynb          # Main notebook
tracks/                      # Generated audio files (created automatically)
soundfont.sf2                # GM SoundFont for MIDI playback
```

Generated tracks are saved in the `tracks/` folder with naming format:
```
{genre}_{mood}_{tempo}bpm_{id}.wav
```

---

## 🎛️ Available Parameters

| Parameter | Options | Default |
|-----------|---------|---------|
| **Mood** | happy, sad, calm, energetic, mysterious | happy |
| **Genre** | pop, rock, jazz, electronic, classical, hiphop, ambient | pop |
| **Tempo** | 60–200 BPM | 120 |
| **Duration** | 1–30 seconds | 15 |
| **Style** | simple, moderate, complex | moderate |
| **Key** | C, G, D, A, E, Am, Em, Dm | C |

---

## 🛠️ Technical Details

### MIDI Generation
- **Tracks**: 4 (melody, chords, bass, drums)
- **Time Signature**: 4/4
- **Note Scheduling**: Non-overlapping, quantized timing
- **Drum Channel**: MIDI Channel 10 (standard percussion)

### AI Model
- Uses DistilGPT2 from Hugging Face for text understanding
- Falls back to rule-based extraction if model fails to load
- Recognizes keywords like "sad rock", "electronic dance", "calm jazz"

### Audio Conversion
- **Sample Rate**: 44100 Hz
- **Format**: 16-bit PCM WAV
- **Synthesis**: FluidSynth with GeneralUser GS SoundFont

---

## 🧪 Testing

The notebook includes built-in tests for:

1. **Music Generator** – Creates a 5-second pop track
2. **AI Extraction** – Processes sample descriptions
3. **Multi-Genre Generation** – Tests 4 different genre/tempo combos

Run the test cells to verify the system works correctly.

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| **MIDI timing errors** | Ensure `adjust_origin=False` in MIDIFile |
| **No audio output** | Check FluidSynth installation and soundfont |
| **Slow generation** | Reduce duration or simplify style |
| **AI model fails to load** | System uses fallback rule-based extraction |

---

## 📄 License

This project is intended for educational and experimental use. The soundfont (`GeneralUser_GS_1.442-MuseScore.sf2`) is used under its respective license.

---

## 🙋‍♂️ Author

**CoverComposer AI** – A stable AI music generation system built with Python and Jupyter.

---

## 🎯 Future Improvements

- [ ] Add deep learning model for parameter extraction
- [ ] Support for more complex chord progressions
- [ ] Real-time audio preview in notebook
- [ ] Export to MP3/OGG formats
- [ ] Web UI with Gradio

---

**Enjoy creating AI-generated music! 🎶**
