# CourseLocalize AI

One-root-folder starter app for English-to-Hindi/Kannada/Tamil/Telugu skill-course localization.

## Layout
- `backend/`: FastAPI API, SQLite, password hashing, user-specific history and terminology, code placeholder protection, quality checks.
- `frontend/`: React + Vite responsive UI.
- `backend/.env.example`: environment configuration.

## Run on Windows PowerShell

Backend terminal:
```powershell
cd backend
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
```
Edit `backend/.env`: set `SECRET_KEY` to a long random value and set `INDICTRANS2_ENDPOINT` to a real compatible IndicTrans2 inference endpoint. The endpoint contract is `POST` JSON `{"text":"...","source_language":"eng_Latn","target_language":"kan_Knda"}` returning `{"translation":"..."}`. Adapt `backend/app/translator.py` if your endpoint uses another schema.
```powershell
uvicorn app.main:app --reload --port 8000
```

Second terminal:
```powershell
cd frontend
npm install
npm run dev
```
Open the Vite URL. API docs: http://127.0.0.1:8000/docs

## Honest limitations
No fake translation is generated. If the inference endpoint is missing or fails, the API reports an error. This starter supports pasted text and TXT/Markdown upload; PDF extraction is not included yet. SQLite is for a local demo, not production multi-user deployment. BPCC is referenced as a resource but is not downloaded or claimed as integrated. Review the official model and dataset licenses/access terms:
- https://github.com/AI4Bharat/IndicTrans2
- https://huggingface.co/datasets/ai4bharat/BPCC

BLEU/chrF++ are only available when a reference translation is supplied and `sacrebleu` is installed. Automated checks do not prove translation accuracy; human review is recommended.
