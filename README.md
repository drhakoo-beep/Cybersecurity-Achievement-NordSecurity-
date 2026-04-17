# Cybersecurity-Achievement-NordSecurity-
NordPass Android - Sensitive Data Exposure and SQLCipher Key Access via RAM

🛡️ NordPass Android - Sensitive Data Exposure and SQLCipher Key Access via RAM

📝 Summary
This research documents a memory security vulnerability I identified in the NordPass Android application that directly threatens the "Zero-Knowledge" architecture. When the application starts the database, the SQLCipher Master Key (64-character hexadecimal key) is briefly exposed in plain text in RAM.

🔍 Technical Analysis
Although the application attempts to delete the key from memory after use, a TOCTOU (Time-of-Check to Time-of-Use) vulnerability exists here. For a millisecond, the key remains unprotected in memory.

Attack Vector: Hooking the sqlite3_key function via automated memory scraping or Frida.

Finding: The 64-character encryption key and PRAGMA configuration lines can be captured in the heap memory as soon as the database arm is opened.

Result: When this key is obtained, the local vault.db file can be completely decrypted without needing the user's Master Password, biometric data, or PIN code.

🚩 Reporting Process (HackerOne)

Status: Closed as Informative.

Response: The company excluded this from the bounty program, stating that "local access" (root or physical access) on the device is required to perform this operation.

Researcher's Note: While the local access requirement reduces the risk, it is technically possible for malware on the device to silently extract this key in the background and leak the entire vault.

Note: These texts are for educational purposes only. 
