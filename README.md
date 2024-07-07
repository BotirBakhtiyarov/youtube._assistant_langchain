## YouTube Assistant Documentation

### Introduction
The YouTube Assistant is a Streamlit-based application designed to provide answers to questions based on video transcripts fetched from YouTube URLs. It leverages LangChain for natural language processing tasks.

### Installation
1. **Clone the repository:**
   ```bash
   git clone https://github.com/BotirBakhtiyarov/youtube._assistant_langchain.git
   cd youtube._assistant_langchain
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

   Ensure you have set up your `.env` file with your OpenAI API key.

### Usage
1. **Run the application:**
   ```bash
   streamlit run main.py
   ```
   This command starts the Streamlit application.

2. **Using the YouTube Assistant:**
   - Enter the YouTube video URL in the sidebar.
   - Type your question about the video in the designated text area.
   - Click the **Submit** button to get a detailed answer based on the video's transcript.

### Files and Structure
- **`main.py`**: Contains the Streamlit application code.
- **`langchain_helper.py`**: Provides helper functions for processing video transcripts and generating responses using LangChain.

### Functionality
- **`create_vector_db_from_youtube_url(video_url)`**:
  - Fetches the transcript from the specified YouTube video URL.
  - Splits the transcript into manageable chunks.
  - Creates a vector database using OpenAI embeddings and FAISS for efficient search.

- **`get_response_from_query(db, query, k)`**:
  - Performs a similarity search in the vector database (`db`) based on the user's query.
  - Utilizes a GPT-3.5 model from OpenAI via LangChain to generate detailed answers using a predefined prompt template.

### Example
An example use case:
```python
import streamlit as st
import langchain_helper as lch

st.title("YouTube Assistant")

with st.sidebar:
    with st.form(key="my_form"):
        youtube_url = st.sidebar.text_area(
            label="What is the YouTube URL?",
            max_chars=50
        )

        query = st.sidebar.text_area(
            label="Ask me about the video?",
            max_chars=50,
            key="query"
        )

        submit_button = st.form_submit_button(label="Submit")

if query and youtube_url:
    db = lch.create_vector_db_from_youtube_url(youtube_url)
    k = 3
    response = lch.get_response_from_query(db, query, k)
    st.subheader("Answer:")
    st.text(textwrap.fill(response, width=80))
```

### Contributing
- If you'd like to contribute to this project, fork the repository and submit a pull request with your proposed changes.
- Ensure any new features or changes are well-documented and tested.

### Contact
- For questions or feedback, contact [Botir Bakhtiyarov](mailto:botirbakhtiyarovb@gmail.com).

---
