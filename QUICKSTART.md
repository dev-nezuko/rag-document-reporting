# First report with synthetic input

Run these commands from the repository root in an isolated Python 3.11+ environment:

```sh
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
# Set the provider key and suitable model names in .env.
python main.py --ingest-file examples/company-brief.md
python main.py --stats
python main.py --query "How did revenue change, and what information is missing?" --output --format markdown
```

The supplied brief is invented. It supports 20% revenue growth and contains no profit or forecast information. Check the generated report against the input rather than assuming the presence of sources proves correctness. Live provider calls were not exercised for this documentation update.

For an API session, run `python -m uvicorn src.api.main:app --host 127.0.0.1 --port 8000` and open localhost:8000/docs. There is no authentication; keep it local. Read the [workflow and limitations](README.md) before ingesting other documents.

The optional `scripts/ingest_sample_data.py` expects an existing `data/raw_data` directory; it does not create a sample dataset. The checked-in `examples/company-brief.md` avoids that prerequisite. Source documents are sent to the configured embedding/chat provider and may incur charges. Keep credentials and real confidential records out of the repository.
