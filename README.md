# 🔓 Password Cracking with JTR & NetworkWalks Tools

**Student:** Ali Imam Khattak
**Program:** Bachelor of Science in Cyber Security (BSCyS)
Program: Cybersecurity

 Platform: NetworkWalks

 Batch: B083C

 Week: 03 Projects: W3-PM1 (Password Cracking with JTR) & W3-PM2 (Password Cracking with NW Tools) 

Tutor: Waqas Karim, CCIE

---

## 📌 Project Overview

This project demonstrates two different approaches to password cracking on password-protected PDF files.

The first approach uses **John the Ripper (JTR)** — a classic offline password-cracking tool — installed on Windows with the Johnny GUI, and then run on Kali Linux when the GUI encountered an issue.

The second approach uses the **NetworkWalks online tools** — Hash Calculator and Password Cracker — which run through a web browser and perform dictionary attacks against extracted hashes.

Both methods follow the same fundamental workflow:

1. Extract the `$pdf$` crackable hash from a locked PDF.
2. Run a dictionary attack against the hash.
3. Recover the plaintext password.
4. Use the recovered password to unlock the PDF.

---

## 🎯 Objectives

* Understand how passwords are protected inside locked PDF files.
* Extract a `$pdf$` hash from a protected PDF.
* Install and use John the Ripper (Johnny GUI + Kali CLI).
* Use the NetworkWalks Hash Calculator and Password Cracker.
* Compare offline CLI password cracking with browser-based dictionary attacks.
* Document the complete password-cracking workflow.
* Understand troubleshooting when a GUI-based tool fails.

---

## 🛠️ Tools Used

| Tool                          | Purpose                                               |
| ----------------------------- | ----------------------------------------------------- |
| Kali Linux                    | Offline password cracking with John the Ripper        |
| John the Ripper (JTR)         | Password cracking tool for hashes and protected files |
| Johnny GUI                    | Graphical front-end for John the Ripper               |
| OnlineHashCrack               | Online PDF hash extraction / pdf2john                 |
| NetworkWalks Hash Calculator  | Browser-based `$pdf$` hash extraction                 |
| NetworkWalks Password Cracker | Browser-based dictionary attack                       |
| Windows 10                    | Host OS for Johnny GUI and browser-based tools        |

---

# 🧩 Locked Lab Files

Three password-protected PDFs were provided for this lab:

| File               | Size             |
| ------------------ | ---------------- |
| My Locked PDF1.pdf | Lab-provided PDF |
| My-Locked-PDF2.pdf | Lab-provided PDF |
| My-Locked-PDF3.pdf | Lab-provided PDF |

The extracted `$pdf$` hash used by John the Ripper is stored as:

`week3/hash1.txt`

---

# 🪜 Activities Performed

# Module 1 — Password Cracking with NetworkWalks Tools (W3-PM2)

## Step 1 — Extract the Hash

The locked PDF was uploaded to the **NetworkWalks Hash Calculator**.

The tool detected that the PDF was encrypted and extracted a crackable hash in `$pdf$` / pdf2john format.

**Evidence:**

* Hash Calculator — PDF1
* Hash Calculator — PDF3

---

## Step 2 — Run the Dictionary Attack

The extracted `$pdf$` hash was pasted into the **NetworkWalks Password Cracker** and the built-in dictionary attack was executed.

### PDF1 Results

The password was successfully cracked:

`good-luck`

A second run returned:

`password1`

### PDF3 Results

The password was successfully cracked:

`1qaz2wsx`

---

## Step 3 — Unlock the PDF

The recovered passwords were used to unlock the protected PDF files.

For example:

`password1`

was successfully used to open the protected PDF.

---

## 🚩 Results — Flags Captured

### Flag 1 — PDF1

Password:

`good-luck`

### Flag 2 — PDF3

Password:

`1qaz2wsx`

### Flag 3 — Final Confirmation

Final confirmation flag was successfully captured using the NetworkWalks tools.

**Evidence:** NetworkWalks Password Cracker screenshots.

---

# Module 2 — Password Cracking with John the Ripper (W3-PM1)

## Step 1 — Install Johnny GUI

Johnny, the graphical front-end for John the Ripper, was downloaded and installed.

After installation, Johnny was opened successfully.

**Evidence:**

* Johnny installer
* Johnny GUI opened

---

## Step 2 — Extract the Hash from the Locked PDF

The **OnlineHashCrack PDF Hash Extractor** was used to upload a locked PDF and extract the crackable `$pdf$` hash.

**Evidence:**

* OnlineHashCrack — PDF input
* OnlineHashCrack — extracted hash

---

## Step 3 — Save the Hash to a File

The extracted hash was copied into a text file.

If a `b'` prefix was present, it was removed according to the lab instructions.

The hash was saved as:

`hash1.txt`

**Evidence:** Notepad — saving `hash1.txt`

---

## Step 4 — Load the Hash into Johnny

Johnny was opened and the **Open password file** option was used to load:

`hash1.txt`

**Evidence:** Johnny — opening `hash1.txt`

---

# ⚠️ Troubleshooting — Johnny GUI Failure

When attempting to start a new attack in Johnny on Windows, the following error appeared:

> "Another johnnyInstaller instance is already running. Wait until it finishes, close it, or restart your system."

The issue appeared to be related to the Johnny GUI and its connection to the underlying `john.exe` process.

Instead of continuing to troubleshoot the GUI, the password-cracking process was moved to **Kali Linux**, where John the Ripper could be executed directly from the command line.

This provided a faster and more reliable way to complete the lab.

---

# Step 5 — Crack with John the Ripper on Kali Linux

The `hash1.txt` file was copied to Kali Linux and saved locally as:

`hash1.txt.save`

The contents of the file were verified using:

```bash
cat hash1.txt.save
```

John the Ripper was then used to crack the hash.

After the attack completed, the recovered password was displayed using:

```bash
john --show hash1.txt.save
```

### Result

The password was successfully recovered:

`good-luck`

John reported:

```text
1 password hash cracked, 0 left
```

**Evidence:** Kali Linux — John the Ripper cracked the hash.

---

# Step 6 — Unlock the PDF

The recovered password:

`good-luck`

was used to open the protected PDF successfully.

**Evidence:** PDF unlocked using `good-luck`.

---

# 🐞 Problems Encountered & Solutions

## Problem 1 — Johnny GUI Error

**Error:**

> "Another johnnyInstaller instance is already running."

### Cause

The Johnny GUI encountered a problem communicating with the underlying John the Ripper process.

### Solution

The task was continued on **Kali Linux** using the `john` command directly instead of relying on the GUI.

### Lesson Learned

Understanding the command-line tool behind a graphical interface is important. When a GUI fails, CLI knowledge provides a reliable alternative and is an important skill in cybersecurity.

---

# 📊 Risk Analysis / Impact

| # | Risk / Finding                                  | Evidence                             | Potential Impact                                           | Risk Level |
| - | ----------------------------------------------- | ------------------------------------ | ---------------------------------------------------------- | ---------- |
| 1 | Weak password `good-luck` was cracked quickly   | JTR + NW Cracker                     | Dictionary words provide little protection                 | High       |
| 2 | Weak password `password1` was cracked instantly | NW Cracker                           | Common password is easy to guess                           | High       |
| 3 | Weak password `1qaz2wsx` was cracked            | NW Cracker                           | Keyboard-pattern passwords are vulnerable                  | High       |
| 4 | Offline hash extraction is straightforward      | OnlineHashCrack + NW Hash Calculator | Anyone with access to the PDF can attempt offline cracking | Medium     |
| 5 | PDF encryption alone is not sufficient          | All three PDFs unlocked              | Weak passwords can undermine encrypted files               | Medium     |

**Risk Level Key:** Critical / High / Medium / Low

These observations were made during an **authorised educational cybersecurity lab**. No real-world systems were targeted.

---

# 💡 Recommendations

* Use long passphrases of **12+ characters**.
* Use a combination of uppercase letters, lowercase letters, numbers and symbols.
* Avoid common dictionary words such as `good-luck`.
* Avoid common passwords such as `password1`.
* Avoid keyboard patterns such as `1qaz2wsx`.
* Use a password manager to generate and securely store strong passwords.
* Enable full-disk encryption on devices containing sensitive information.
* Perform password-strength audits on encrypted files shared by an organisation.
* Remember that encryption is only as strong as the password protecting it.

---

# 💡 What I Learned

Through this project, I learned:

### 1. How PDF Password Hashes Work

I learned how password-protected PDFs can contain crackable `$pdf$` hashes that can be extracted using tools such as pdf2john.

### 2. How Dictionary Attacks Work

I learned how password crackers test words from a wordlist against the target hash until the correct password is found.

### 3. Importance of CLI Knowledge

When the Johnny GUI failed, I was able to continue the task using John the Ripper directly on Kali Linux.

This showed me that understanding the underlying command-line tools is more important than relying only on a graphical interface.

### 4. Weak Passwords Can Be Cracked Easily

The lab demonstrated that passwords such as:

* `good-luck`
* `password1`
* `1qaz2wsx`

are weak and can be recovered quickly using dictionary-based attacks.

### 5. Troubleshooting Is Part of Cybersecurity

The Johnny GUI error was documented as part of the project. Instead of stopping when the GUI failed, I used Kali Linux and the command-line version of John the Ripper to complete the task.

---

# 🔐 Security & Ethical Use

This project was completed as part of an **authorised educational cybersecurity lab at NetworkWalks**.

All password-cracking activities were performed against lab-provided encrypted PDF files specifically supplied for this exercise.

No real-world systems, accounts or user data were targeted.

No unauthorised access or credential attacks against live systems were performed.

The techniques demonstrated in this project are intended for defensive cybersecurity education and for understanding how weak passwords can be identified and strengthened.

---

# 👤 Author

**Ali Imam Khattak**

Bachelor of Science in Cyber Security (BSCyS)
Shifa Tameer-e-Millat University (STMU), Islamabad

**Cybersecurity Program — NetworkWalks**
**Batch:** B083C

**LinkedIn:** Ali Imam Khattak

---

# 📌 Project Information

**Program:** Cybersecurity at NetworkWalks
**Student:** Ali Imam Khattak
**University:** Shifa Tameer-e-Millat University (STMU), Islamabad
**Batch:** B083C
**Week:** 03
**Projects:** W3-PM1 (JTR) & W3-PM2 (NW Tools)
**Tutor:** Waqas Karim, CCIE

**Repository:** GitHub

---

## End of Report
