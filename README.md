# Network Walks Cybersecurity Internship 2026 — Week 3 (W3-PM1)
**Topic:** Offline Password Cracking & Hash Extraction with John the Ripper & Johnny GUI  
**Author:** David Mukoshi  

## Overview
This lab demonstrates practical cryptographic hash extraction and offline dictionary/rule-based password recovery against password-protected PDF documents using **John the Ripper (`1.9.0-jumbo-1`)** integrated with **Johnny GUI** on Windows.

## Lab Workflow & Methodology

### 1. Tool Configuration
- Deployed `john-1.9.0-jumbo-1-win64` alongside `johnny_2.2_win`.
- Configured the binary path (`C:/john/john-1.9.0-jumbo-1-win64/run/john.exe`) in Johnny GUI **Settings** and verified OpenMP/AVX2 engine detection.

<!-- Paste/Drop Screenshot 1 (Johnny Settings Detected) below this line -->
![Johnny GUI Settings Configuration](./images/johnny-settings.png)

### 2. Hash Extraction
- Extracted `$pdf$` hash strings from three encrypted target PDFs (`PDF 1`, `PDF 2`, and `PDF 3`) using OnlineHashCrack's PDF Hash Extractor (`Standard Security Handler V4 / Revision 4, 128-bit`).

<!-- Paste/Drop Screenshot 2 (OnlineHashCrack Extraction) below this line -->
![OnlineHashCrack PDF Hash Extraction](./images/pdf1-hash-extract.png)

### 3. Password Recovery & Flag Verification
- Loaded extracted hashes into Johnny GUI (`format=PDF`) and executed wordlist attacks to recover the plaintext passwords.
- Unlocked each encrypted PDF document with its recovered password to retrieve the embedded CTF flags.

<!-- Paste/Drop Screenshot 3 (Cracked Passwords & Flags) below this line -->
![Cracked Password in Johnny GUI](./images/johnny-cracked.png)
![Captured CTF Flag](./images/flag-captured.png)

## Results & Captured Flags

| Target Document | Hash Format | Recovered Password | Captured Flag |
| :--- | :--- | :--- | :--- |
| `My Locked PDF1.pdf` | `$pdf$4*4*128*` | `good-luck` | `nw{cybersecurity_flag_captured_2608}` |
| `PDF 2` | `$pdf$4*4*128*` | `password1` | `nw{networkwalks_persistence_jtr_270521}` |
| `PDF 3` | `$pdf$4*4*128*` | `1qaz2wsx` | `nw{networkwalks_flag_260821_1}` |

## Key Security Takeaways & Remediation
- **Vulnerability:** All three recovered passwords (`good-luck`, `password1`, and the keyboard-walk pattern `1qaz2wsx`) fall immediately to standard dictionary and keyboard-pattern wordlists despite 128-bit PDF encryption.
- **Remediation:** Enforce high-entropy passphrases (14+ characters, avoiding keyboard walks and common dictionary terms) and upgrade document encryption to AES-256 (PDF 2.0 / Acrobat X+) to increase computational cracking resistance.
