# Resume Evaluator

An AI-powered resume screening tool that parses job descriptions and resumes, then ranks candidates by match score using the **Groq LLM API**.

## What It Does

1. **Parses the job description** — extracts role, required/preferred skills, experience, education, and responsibilities into structured JSON.
2. **Reads resumes** from the `resumes/` folder (supports `.pdf` and `.docx`).
3. **Parses each resume** — extracts name, contact info, skills, experience, education, projects, and certifications.
4. **Scores each candidate** — compares the resume against the job description and returns a match percentage with detailed feedback.
5. **Prints a ranked leaderboard** — highlights the top 2 and lowest 2 candidates.

## Project Structure

```
resume-evaluator/
├── resumes/              # Drop PDF or DOCX resumes here
├── src/resume_evaluator/ # Package entry point
├── resume_parser.py      # Main script
├── pyproject.toml        # Project metadata & dependencies
├── .env                  # API keys
└── README.md
```

## Setup

### 1. Clone & install dependencies

```bash
uv sync
```

### 2. Configure environment variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=openai/gpt-oss-20b   # optional, this is the default
```

### 3. Add resumes

Place candidate resumes (`.pdf` or `.docx`) into the `resumes/` folder.

### 4. Set the job description

Edit the `jobDescription` string inside [`resume_parser.py`](resume_parser.py) with the target job posting.

### 5. Run

```bash
python resume_parser.py
```

## Dependencies

| Package        | Purpose                        |
|----------------|-------------------------------|
| `groq`         | LLM API client                |
| `pypdf`        | PDF text extraction           |
| `python-docx`  | DOCX text extraction          |
| `pydantic`     | Structured data validation    |
| `python-dotenv`| Environment variable loading  |

## Output Example

```
TOP 2 CANDIDATES
Alice Smith - 87.0 %
{'matching_skills': [...], 'missing_skills': [...], 'verdict': '...'}

LOWEST 2 CANDIDATES
Bob Jones - 42.0 %
{'matching_skills': [...], 'missing_skills': [...], 'verdict': '...'}
```

## Notes

- A 5-second delay is added between LLM calls to respect API rate limits.
- The model can be overridden via the `GROQ_MODEL` environment variable.
