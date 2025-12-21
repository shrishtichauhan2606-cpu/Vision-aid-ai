import streamlit as st
import google.generativeai as genai
from PIL import Image

# 1. API Configuration
# Get your API key from https://aistudio.google.com/
API_KEY = "YOUR_GEMINI_API_KEY" 
genai.configure(api_key=API_KEY)

# 2. Model Initialization
# Use Gemini 1.5 Flash for high-speed multimodal tasks
model = genai.GenerativeModel('gemini-1.5-flash')

# 3. VisionAid Logic (The Golden Prompt)
SYSTEM_PROMPT = """
Analyze this image from the perspective of a navigation assistant for the visually impaired.
Perform the following:
1. OVERVIEW: One concise sentence summarizing the location.
2. SAFETY: List any obstacles, hazards, or moving objects in the immediate path.
3. TEXT: Extract and read all visible signs, room numbers, or labels.
4. SPATIAL: Describe the layout (e.g., 'a door is at 2 o'clock').
Use clear, instructional language.
"""

# 4. Streamlit Interface
st.set_page_config(page_title="VisionAid AI", layout="centered")

st.header("👁️ VisionAid: Multimodal Environment Narrator")
st.markdown("---")

# Image Input
source = st.radio("Input Source:", ["Upload Photo", "Use Camera"])
if source == "Upload Photo":
    img_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
else:
    img_file = st.camera_input("Take a snapshot of the environment")

if img_file:
    raw_img = Image.open(img_file)
    st.image(raw_img, caption="Environment Captured", use_container_width=True)
    
    if st.button("Narrate Scene"):
        with st.spinner("Processing visual data..."):
            try:
                # Generate AI response using Multimodal capabilities
                response = model.generate_content([SYSTEM_PROMPT, raw_img])
                
                # Output Results
                st.subheader("🔊 Scene Narration")
                st.info(response.text)
                
            except Exception as e:
                st.error(f"Execution Error: {str(e)}")

st.markdown("---")
st.caption("Multimodal Architecture | Gemini 1.5 Flash Engine")
