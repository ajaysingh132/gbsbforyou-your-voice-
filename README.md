# gbsbforyou-your-voice-
अपनी और अपनों की आवाज संरक्षित करें 
ok
# =============================================
# gbsbforyou — Your Voice For You
# AI Voice Cloning Tool — Preserve Heritage, Empower Education, Celebrate Culture
# No Vercel — No Deploy — Just Run Anywhere!
# =============================================

# Step 1: Install Required Libraries
!pip install TTS gradio

# Step 2: Import Libraries
import gradio as gr
from TTS.api import TTS

# Step 3: Load Voice Cloning Model (Supports Indian Voices & Accents)
print("🔄 Loading Voice Cloning Model — Please Wait...")
tts = TTS(model_name="tts_models/multilingual/multi-dataset/your_tts", progress_bar=True)
print("✅ Model Loaded Successfully!")

# Step 4: Define Function to Clone Voice and Generate Audio
def clone_and_speak(reference_audio, text):
    """
    Clone voice from reference audio and generate speech from text.
    """
    try:
        output_path = "output.wav"
        print(f"🗣️ Generating speech in cloned voice...")
        tts.tts_to_file(
            text=text,
            speaker_wav=reference_audio,
            language="hi",  # Supports Hindi, English, and more
            file_path=output_path
        )
        print("✅ Speech Generated Successfully!")
        return output_path
    except Exception as e:
        print(f"❌ Error: {e}")
        return None

# Step 5: Create Gradio Interface — Simple, Beautiful, Mobile-Friendly
with gr.Blocks(
    title="gbsbforyou — Your Voice For You",
    theme=gr.themes.Soft()
) as demo:
    # Header
    gr.Markdown("# 🎙️ gbsbforyou — Your Voice For You")
    gr.Markdown("### *आवाज़ क्लोन करो — विरासत बचाओ — शिक्षा बदलो*")
    gr.Markdown("---")

    # Instructions
    gr.Markdown("### 📌 कैसे यूज़ करें?")
    gr.Markdown("1. 🎤 60 सेकंड की अपनी/दादी/माँ/दोस्त की आवाज़ अपलोड करें (MP3/WAV)\n2. 📝 वह टेक्स्ट टाइप करें जो आप उस आवाज़ में सुनना चाहते हैं\n3. ▶️ 'प्ले' दबाएं — आवाज़ सुनें!\n4. ⬇️ 'डाउनलोड' दबाएं — MP3 सेव करें!")

    # Input Components
    with gr.Row():
        audio_input = gr.Audio(
            label="🎤 अपनी आवाज़ अपलोड करें (60s तक)",
            type="filepath",
            elem_id="audio-upload"
        )
        text_input = gr.Textbox(
            label="📝 क्या बोलना चाहते हैं?",
            placeholder="मेरी दादी की कहानी — गेंद-बाज़ शहज़ादी...",
            lines=5,
            elem_id="text-input"
        )

    # Output Component
    output_audio = gr.Audio(
        label="🔊 आउटपुट — आपकी आवाज़ में!",
        elem_id="audio-output"
    )

    # Generate Button
    btn = gr.Button("▶️ प्ले — मेरी आवाज़ में सुनो!", variant="primary")
    btn.click(
        fn=clone_and_speak,
        inputs=[audio_input, text_input],
        outputs=output_audio
    )

    # Footer
    gr.Markdown("---")
    gr.Markdown("### 📁 डाउनलोड करें — और [Digital Voice Archive](https://drive.google.com) में सेव करें")
    gr.Markdown("### 📣 #AwazonKaKhazana — दादा-दादी की आवाज़, बच्चों का भविष्य, भारत की विरासत")
    gr.Markdown("*(हम आवाज़ बेचते नहीं — संजोते हैं)*")
    gr.Markdown("© 2025 gbsbforyou — Your Voice For You | Email: ajaychinty3@gmail.com")

# Step 6: Launch Tool — Local + Public URL
print("🚀 Launching Tool — Please Wait...")
demo.launch(share=True)
print("🎉 Tool is Live! Check the Public URL below.")
