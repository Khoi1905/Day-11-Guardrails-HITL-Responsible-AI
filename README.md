# Day 11 - Guardrails, HITL & Responsible AI

Completed lab implementation for securing a VinBank assistant with Google ADK,
Gemini, NeMo Guardrails, automated red teaming, and human-in-the-loop routing.

## Objectives

- Understand why guardrails are mandatory for AI products
- Implement input guardrails (injection detection, topic filter)
- Implement output guardrails (content filter, LLM-as-Judge)
- Use NeMo Guardrails (NVIDIA) with Colang
- Design HITL workflow with confidence-based routing
- Perform basic red teaming

## Completed Deliverables

- All 13 lab TODOs implemented in `src/`.
- Completed notebook: `notebooks/lab11_guardrails_hitl_completed.ipynb`.
- Security report and HITL flowchart: `LAB_REPORT.md`.
- Offline regression tests: `tests/test_lab.py`.

## Project Structure

```
Day-11-Guardrails-HITL-Responsible-AI/
├── notebooks/
│   ├── lab11_guardrails_hitl.ipynb
│   └── lab11_guardrails_hitl_completed.ipynb
├── src/
│   ├── main.py                    # Entry point
│   ├── core/
│   │   ├── config.py              # API key setup, allowed/blocked topics
│   │   └── utils.py               # chat_with_agent() helper
│   ├── agents/
│   │   └── agent.py               # Unsafe & protected agent creation
│   ├── attacks/
│   │   └── attacks.py             # Adversarial prompts and AI red teaming
│   ├── guardrails/
│   │   ├── input_guardrails.py    # Injection detection, topic filter, ADK plugin
│   │   ├── output_guardrails.py   # Redaction, LLM-as-Judge, ADK plugin
│   │   └── nemo_guardrails.py     # NeMo Guardrails with Colang
│   ├── testing/
│   │   └── testing.py             # Before/after comparison and test pipeline
│   └── hitl/
│       └── hitl.py                # Confidence router and HITL design
├── tests/
│   └── test_lab.py
├── .env.example
├── LAB_REPORT.md
├── requirements.txt
└── README.md
```

## Setup

### Local Windows (recommended)

Use Python 3.11. NeMo's `annoy` dependency may require Microsoft C++ Build
Tools on Windows.

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
Copy-Item .env.example .env
```

Set `GOOGLE_API_KEY` in `.env`. The `.env` file is excluded from Git.

```powershell
cd src

# Run the full lab
..\.venv\Scripts\python.exe main.py

# Or run specific parts
..\.venv\Scripts\python.exe main.py --part 1
..\.venv\Scripts\python.exe main.py --part 2
..\.venv\Scripts\python.exe main.py --part 3
..\.venv\Scripts\python.exe main.py --part 4
```

### Offline Verification

These checks do not consume Gemini quota:

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
.\.venv\Scripts\python.exe -m pip check
```

The verified result is **9/9 tests passing** with no dependency conflicts.

## Notes

- Parts 1-3 call Gemini and consume API quota. Part 4 runs without an API key.
- The free-tier daily quota may prevent repeating the entire live test sequence
  on the same day.
- See `LAB_REPORT.md` for actual before/after results, limitations, and HITL
  decision points.

## References

- [OWASP Top 10 for LLM](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails)
- [Google ADK Documentation](https://google.github.io/adk-docs/)
- [Official Google's Gemini cookbook](https://github.com/google-gemini/cookbook/blob/main/examples/gemini_google_adk_model_guardrails.ipynb)
- [AI Safety Fundamentals](https://aisafetyfundamentals.com/)
- [AI Red Teaming Guide](https://github.com/requie/AI-Red-Teaming-Guide)
- [antoan.ai - AI Safety Vietnam](https://antoan.ai)

