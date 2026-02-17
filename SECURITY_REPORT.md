# 📱 Mobile Application Security Lab & Vulnerability Research

This repository documents my professional environment and methodology for mobile security auditing. It showcases my ability to bridge **software development** and **security engineering** by performing deep-dive analysis of Android binaries.

## 🛠 Security Engineering Stack
* **Containerization:** Docker Desktop for consistent, isolated environment deployment.
* **Static Analysis (SAST):** **MobSF** for automated binary deconstruction and manifest auditing.
* **Manual Code Review:** **JADX-GUI** for reverse engineering and logic flow analysis.
* **Dynamic Analysis:** **Frida** (Runtime instrumentation) for bypassing security controls (In Progress).
* **Backend Auditing:** **Bandit** for identifying security flaws in Python-based components.

---

## 🚀 Lab Infrastructure
### Containerized Security Environment
<img width="1352" height="878" alt="Снимок экрана 2026-01-21 в 5 50 05 PM" src="https://github.com/user-attachments/assets/88fd0fbd-d7e2-4685-aade-9050ad75d905" />
### Containerized Security Environment
I utilized **Docker** to deploy a hardened instance of the Mobile Security Framework (MobSF). This approach ensures environment isolation and prevents host machine contamination during analysis.
* **Status:** Operational (Healthy).
* **Access:** Local instance mapped to `http://localhost:8000`.

---

## 📊 Deep-Dive Audit: InsecureBankv2 Case Study

To validate the lab's efficacy, I performed a comprehensive security assessment of the **InsecureBankv2** application, mapping findings to the **OWASP Mobile Top 10** risks.

### 1. Risk Profile & Executive Summary
* **Security Score:** **28/100** (Critical Risk Assessment).
* **Package:** `com.android.insecurebankv2`.
* **Attack Surface:** High number of exported components and dangerous permission requests.

### 2. Manifest & Permission Auditing
Automated analysis revealed a significant over-provisioning of permissions, violating the **Principle of Least Privilege**:
* **Dangerous Permissions:** `SEND_SMS`, `READ_CONTACTS`, `ACCESS_COARSE_LOCATION`. These create vectors for data exfiltration and unauthorized communication.
* **Identity Risks:** Permissions like `GET_ACCOUNTS` were flagged as potential privacy violations.

### 3. Component Exposure (IPC Risks)
A critical vulnerability was identified in the app's Inter-Process Communication (IPC) design:
* **Exported Activities (4/10):** These are accessible by any other application on the device, potentially leading to **Intent Spoofing**.
* **Exported Providers (1/1):** Critical risk of database manipulation or sensitive data theft.

---

## 🛡 Strategic Remediation & Hardening
<img width="1352" height="878" alt="Снимок экрана 2026-01-21 в 5 51 35 PM" src="https://github.com/user-attachments/assets/8f830acc-47e3-4e26-a367-6586c0999674" />

Based on the audit, I propose the following security enhancements:

1. **Enforce Component Isolation:** Explicitly set `android:exported="false"` in the `AndroidManifest.xml` for all internal components.
2. **Permission Hardening:** Refactor the manifest to request only the minimum set of permissions required for core functionality.
3. **Data-in-Transit Protection:** Implement a **Network Security Configuration** (NSC) to disable cleartext traffic and enforce strict HTTPS.
4. **Binary Obfuscation:** Implement R8/ProGuard and runtime checks to hinder manual analysis via JADX/Frida.

---

## 🎓 Academic Context
This research is part of my **Cybersecurity & Information Assurance** degree at **WGU**. It demonstrates proficiency in identifying architectural flaws and providing actionable remediation for development teams.
