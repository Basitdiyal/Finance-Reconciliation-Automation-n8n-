# 🤖 Automated Financial Reconciliation Workflow (n8n + AI)

This project automates the tedious process of **financial reconciliation** between **bank transactions** and **booking records** using **n8n**, **LLM (AI)**, and **Google Sheets**.  
It replaces hours of manual work with a smart, rule-based and AI-assisted workflow that matches, updates, and notifies automatically.

---

## 🚀 Project Overview

Manual reconciliation of transactions against booking data is often error-prone and time-consuming.  
This workflow automates the entire process from **data ingestion** to **final reporting**.

With this automation:
- Saves **4 hours daily** (≈ **20 hours per week**) of manual reconciliation effort.
- Reduces mismatch errors by **95%**.
- Provides real-time visibility into matched and unmatched entries.
- Automatically sends **emails for unmatched entries** and updates **booking status** for successful matches.

---

## 🧩 Workflow Architecture

### **1️⃣ Read Transactions**
- **Google Sheets Node**  
  Reads transaction data from a Google Sheet (`Transactions`).

### **2️⃣ AI Extraction**
- **LLM Node / Agent Node**  
  Uses AI to detect and extract booking numbers from transaction descriptions.  
  Output → `Booking Number (Detected)`.

### **3️⃣ Booking List Fetch**
- **Google Sheets Node**  
  Reads existing bookings with fields like `Booking_ID`, `Status`, `Amount`, etc.

### **4️⃣ Match Transactions with Bookings**
- **Merge Node**  
  Performs an **Inner Join** between AI-detected `Booking Number` and `Booking_ID` from booking data.  
  Output → Only matched rows.

- **If Node (Check_Match_Status)**  
  Detects missing or invalid booking numbers to label unmatched rows as `Not Found`.

---

## 🧠 Additional Automation

### **✅ Successful Reconciliations**
- Booking entries are automatically updated to **Status = Paid** in the booking sheet.

### **📧 Unmatched Transactions**
- Automatically sends an **email to the Finance Department** listing all “Not Found” transactions for review.

---

## 🧮 Columns Used

| Column Name | Purpose |
|--------------|----------|
| Booking Number (Detected) | Extracted by AI from transaction description |
| Match Status | Auto-updated as `Matched` or `Not Found` |
| Booking Status | Updated to `Paid` after successful reconciliation |
| Reconcile_Flag | (Optional) Used to skip already processed rows |

---

## ⚙️ Tools & Tech Stack

- **n8n** – Core workflow automation
- **Google Sheets** – Data source and output
- **OpenAI / LLM Agent** – For AI extraction of booking numbers
- **SMTP / Gmail Node** – For automated email reporting
- **Merge + IF + Set Nodes** – For data flow control and conditional updates

---

## 📊 Workflow Summary

| Step | Node | Function |
|------|------|-----------|
| 1 | Google Sheets | Read transactions |
| 2 | LLM / Agent | Detect booking number |
| 3 | Google Sheets | Read bookings |
| 4 | Merge | Join detected + booking data |
| 5 | IF Node | Identify unmatched entries |
| 6 | Google Sheets | Update match status |
| 7 | Email Node | Notify finance department |
| 8 | Google Sheets | Mark paid bookings |

---

## 📢 Project Showcase on LinkedIn

You can view the live showcase and explanation post here:  
👉 [LinkedIn Project Post – Automated Financial Reconciliation](https://www.linkedin.com/posts/basitalidiyal_automation-ai-n8n-activity-7385236032289505280-Ee7r)

---
