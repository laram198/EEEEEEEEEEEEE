# 📄 AI Resume ATS Checker

Upload a resume (PDF, DOCX or TXT) and get an **estimated ATS score**, a category breakdown, prioritised improvements, keyword suggestions and rewritten bullet examples. Optionally paste a job description to get a tailored **job match** score.

Built with [Streamlit](https://streamlit.io) and Google's Gemini Flash model.

## Features

- PDF, DOCX and TXT resume support (up to 5 MB)
- Overall ATS score (weighted average of category scores, calculated in code)
- Breakdown: formatting, keywords, achievements, clarity, completeness, job match
- Prioritised improvements (high / medium / low) with concrete fixes
- Missing keywords and before/after bullet rewrites
- Downloadable Markdown report

> **Note:** the score is an AI-generated estimate, not the output of a real ATS. Use it as guidance.

## Project structure

```
resume-ats-analyzer/
├── app.py            # Streamlit app
├── requirements.txt  # Python dependencies
└── README.md
```

## Run locally

1. **Get a Gemini API key** (free tier available) at <https://aistudio.google.com/apikey>.

2. **Install dependencies** (Python 3.10+ recommended):

   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Provide your API key**, using either option:

   - Environment variable:
     ```bash
     export GEMINI_API_KEY="your-key"      # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
     ```
   - Or create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your-key"
     ```
   - Or just paste the key into the sidebar when the app starts.

4. **Start the app:**

   ```bash
   streamlit run app.py
   ```

   It opens at <http://localhost:8501>.

## Configuration

| Setting          | Where                       | Default            |
| ---------------- | --------------------------- | ------------------ |
| `GEMINI_API_KEY` | secrets / env var / sidebar | (required)         |
| `GEMINI_MODEL`   | secrets / env var / sidebar | `gemini-3.5-flash` |

Model names change over time. If you see a "model not found" error, check the current names at <https://ai.google.dev/gemini-api/docs/models> and set `GEMINI_MODEL`.

## Deploy on Streamlit Community Cloud

1. Push this project to a GitHub repository (**never commit your API key**; `.streamlit/secrets.toml` must be in `.gitignore`).
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app** → choose your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**. You get a public `*.streamlit.app` URL.

## Privacy

Resumes are processed in memory and sent to the Gemini API for analysis. The app does not store uploaded files. Review Google's API data-use terms before analysing sensitive documents.

## Troubleshooting

- **"Very little text could be extracted"**: the PDF is probably a scanned image. Export a text-based PDF or DOCX.
- **API errors / 429**: you may have hit the free-tier rate limit. Wait a minute and retry.
- **Invalid API key**: regenerate it in Google AI Studio and update your secret.

## License

MIT, so use it freely.
