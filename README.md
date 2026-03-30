import streamlit as st
from openai import OpenAI

# Initialize OpenAI client
client = OpenAI(api_key="YOUR_API_KEY_HERE")

# App Title
st.title("🧠 Medical Terminology Translator")

st.write("Enter a medical term to get a simple explanation.")

# User Input
term = st.text_input("Enter Medical Term")

# Button
if st.button("Translate"):
    if term:
        with st.spinner("Explaining..."):
            response = client.chat.completions.create(
                model="gpt-4.1-mini",
                messages=[
                    {"role": "system", "content": "You are a medical assistant. Explain medical terms in simple, short, beginner-friendly language."},
                    {"role": "user", "content": f"Explain the medical term '{term}' in simple words."}
                ]
            )
            
            result = response.choices[0].message.content
            
            st.success("Explanation:")
            st.write(result)
    else:
        st.warning("Please enter a term.")
