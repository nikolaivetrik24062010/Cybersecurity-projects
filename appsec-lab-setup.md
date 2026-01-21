# AppSec Local Environment Setup (macOS, Homebrew, Python)

## Goal
Prepare a **production-grade local environment** for Application Security practice:
- SAST / DAST tooling
- Secure API testing
- Reproducible Python setup
- No system Python breakage (PEP 668 compliant)

---

## 1. Homebrew Installation

Homebrew installed to manage system-level tools safely:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Add Homebrew to PATH:

echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

Verification:

brew --version
which brew

Result:
	•	Homebrew installed in /opt/homebrew
	•	Managed Python available

⸻

2. Python State (Correct & Expected)

System Python is externally managed by Homebrew (PEP 668).

Verification:

which python3
python3 --version
which pip3
pip3 --version

Result:
	•	Python 3.14.x (Homebrew)
	•	pip blocked for system installs (expected behavior)

Important:
System-wide pip install is intentionally blocked to prevent OS / Homebrew breakage.

⸻

3. AppSec Virtual Environment (Best Practice)

Created isolated workspace for security tooling:

mkdir ~/appsec
cd ~/appsec

python3 -m venv venv
source venv/bin/activate

Verification:

which python
python --version

Result:

~/appsec/venv/bin/python
Python 3.14.2


⸻

4. AppSec Tooling Installed (Inside venv)

Installed core AppSec tools only inside virtual environment:

pip install bandit flask fastapi requests python-dotenv PyJWT

Installed tools include:
	•	Bandit — SAST for Python
	•	Flask / FastAPI — insecure & secure API demos
	•	Requests — API testing
	•	PyJWT — JWT security testing
	•	python-dotenv — secrets handling

Verification:

bandit --version
flask --version

Result:
	•	Tools installed and executable from venv/bin
	•	No system-level contamination

⸻

5. Compliance & Security Rationale

This setup:
	•	Complies with PEP 668
	•	Prevents breaking Homebrew Python
	•	Mirrors enterprise AppSec / CI/CD practices
	•	Enables reproducible environments via venv

Talking point for interviews:

I use Homebrew-managed Python and isolate all AppSec tooling in virtual environments to comply with PEP 668 and avoid system-level dependency conflicts.

⸻

6. Environment Status (Final)

✅ Homebrew configured
✅ Python 3.14.x managed safely
✅ Virtual environment active
✅ AppSec tools installed correctly
✅ Ready for SAST / DAST / API security labs

⸻

7. Next Practical Steps

Recommended progression:
	1.	Bandit (SAST) — insecure code → finding → fix
	2.	FastAPI + JWT — IDOR & auth misconfigurations
	3.	Burp Suite / OWASP ZAP — DAST against local API
	4.	AWS Cognito — MFA, token flow, misconfig analysis

