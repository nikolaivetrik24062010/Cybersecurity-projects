# Mobile Application Security Auditing Lab

This repository documents my professional environment for mobile application security research and vulnerability assessment.

## 🛠 Technical Stack
* **Docker Desktop**: Used for container orchestration and environment isolation.
* **MobSF (Mobile Security Framework)**: A comprehensive tool for automated SAST (Static Analysis) and DAST (Dynamic Analysis) of mobile applications.
* **Bandit**: Specialized tool for performing static analysis on Python-based backend components.
* **Git**: Used for repository management and source code versioning.

---

## 🚀 Lab Deployment

### Containerization
<img width="1352" height="878" alt="Снимок экрана 2026-01-21 в 5 50 05 PM" src="https://github.com/user-attachments/assets/88fd0fbd-d7e2-4685-aade-9050ad75d905" />
The security environment is hosted within a **Docker** container to ensure a consistent and isolated testing platform. 
* **Container Status**: Healthy and operational.
* **Port Mapping**: Local access via `http://localhost:8000`.



### Automated Framework (MobSF)
I successfully deployed the MobSF framework to handle automated binary deconstruction and manifest analysis.



---

## 📊 Case Study: InsecureBankv2 Audit Results

To validate the lab's capabilities, I performed a full security audit on a sample banking application. 

### Audit Summary
<img width="1352" height="878" alt="Снимок экрана 2026-01-21 в 5 51 35 PM" src="https://github.com/user-attachments/assets/8f830acc-47e3-4e26-a367-6586c0999674" />
* **Security Score**: 28/100 (Critical Risk).
* **Package Name**: `com.android.insecurebankv2`.
* **Main Findings**: Multiple high-severity misconfigurations.



### Vulnerability Analysis:
* **Dangerous Permissions**: The app requests high-risk permissions such as `SEND_SMS`, `READ_CONTACTS`, and `ACCESS_COARSE_LOCATION`.
* **Exported Components**: Several Activities and Providers are marked as "Exported," allowing potential unauthorized access by third-party applications.
* **Insecure Manifest**: Basic security flags like `allowBackup` were found improperly configured.



---

## 🛡 Remediation Strategies
1. **Apply Principle of Least Privilege**: Remove all unnecessary permissions from the `AndroidManifest.xml`.
2. **Component Isolation**: Explicitly set `android:exported="false"` for all internal-only components.
3. **Data Protection**: Implement strict Network Security Configurations to enforce HTTPS and prevent cleartext traffic.
