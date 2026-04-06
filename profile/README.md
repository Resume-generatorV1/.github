# CV Generator

A modular, intelligent CV generation toolkit built in Python. The project is designed around a pipeline of composable modules — starting with automated skill extraction from job descriptions, and expanding toward full CV parsing, tailoring, and generation.

---

## Project Status

| Module | Status | Description |
|---|---|---|
| `skill_extractor` | Completed | Extract & rank tech skills from job descriptions |
| CV Parser | Planned | Parse existing CVs into structured data |
| CV Tailor | Planned | Match CV skills to a target job description |
| CV Generator | Planned | Generate/render a polished CV document |

---

## Modules

### `skill_extractor`

A fully local, LLM-free pipeline for extracting and ranking tech keywords from job descriptions. Built on spaCy v3 and the [ESCO taxonomy](https://esco.ec.europa.eu/en/use-esco/download) (13,890+ skills).

---

## Requirements

- Python 3.10+
- spaCy 3.x (`pip install spacy`)
- spaCy model: `en_core_web_lg` (`python -m spacy download en_core_web_lg`)
- ESCO skills CSV (see Setup above)
