# 💰 Finance Reconciliation Automation (n8n)

This project automates the **finance reconciliation process** using **n8n**, **Google Sheets**, and **AI integration** to reduce manual workload, increase accuracy, and provide real-time insights into unmatched transactions.  

---

## 🚀 Overview

Finance reconciliation — comparing **bank transactions** with **internal booking records** — is often a time-consuming, error-prone task.  
This workflow was built to **automate** that process end-to-end using **n8n**, eliminating repetitive data matching and manual status updates.

By implementing this solution, finance teams can save **up to 4 hours per day (≈20 hours weekly)** on manual reconciliation tasks.

---

## 🧩 Workflow Summary

The automation consists of **three main stages**:

### 1️⃣ Data Import  
- Bank statements are uploaded to a **Google Drive** folder.  
- Data is automatically cleaned and saved to a **Google Sheet (Transactions)**.  
- A second Google Sheet (**Bookings**) holds expected inflows from internal systems.  

### 2️⃣ Data Processing & AI Extraction  
- The **LLM (AI Agent Node)** reads transaction descriptions to detect booking numbers.  
- It extracts or “cleans” booking numbers using fuzzy matching and pattern recognition.  
- Detected booking numbers are stored in a new column: `Booking Number (Detected)`.

### 3️⃣ Matching & Reconciliation  
- Using a **Merge Node**, the workflow compares `Booking Number (Detected)` from transactions with `Booking_ID` from the bookings sheet.  
- A **Match Status** column is updated:
  - `Matched` → when booking number exists in both sheets  
  - `Not Found` → when no corresponding record exists  

### 4️⃣ Notifications & Updates  
- **Email Node** automatically sends unmatched (Not Found) transactions to the finance team for review.  
- For successfully reconciled entries, the **Bookings Sheet** `Status` column is updated to `Paid`.  
- The system runs daily, ensuring real-time reconciliation.

---

## 🛠️ Tools & Nodes Used

| Step | Node | Function |
|------|------|-----------|
| 1 | **Google Drive** | Watch for uploaded bank statements |
| 2 | **Google Sheets (Transactions)** | Read and write transaction data |
| 3 | **AI Agent / OpenAI Node** | Extract booking numbers from payment descriptions |
| 4 | **IF Node** | Separate detected and non-detected booking numbers |
| 5 | **Merge Node (Inner Join)** | Match detected booking numbers with booking list |
| 6 | **Set Node** | Add or update custom columns (`Booking Number (Detected)`, `Match Status`) |
| 7 | **Google Sheets (Update Rows)** | Write back reconciliation results |
| 8 | **Email Node** | Notify finance team of unmatched records |
| 9 | **Google Sheets (Update Rows)** | Mark matched bookings as Paid |

---

## 📊 Example Data

### **Transactions Sheet**
| Date | Description | Amount | Booking Number (Detected) | Match Status |
|------|--------------|--------|----------------------------|--------------|
| 2025-10-01 | Payment from John Doe #BKG-101 | 500 | BKG-101 | Matched |
| 2025-10-02 | Deposit from Ali | 450 | - | Not Found |

### **Bookings Sheet**
| Booking_ID | Customer | Amount | Status |
|-------------|-----------|--------|--------|
| BKG-101 | John Doe | 500 | Paid |
| BKG-102 | Sara Khan | 450 | Pending |

---

## ⚙️ Automation Trigger

The workflow is triggered **automatically** when:  
- A new bank statement file is uploaded to the specified Google Drive folder.  
- Or manually triggered inside n8n for testing/debugging.  

---

## 📧 Notification Example

**Subject:** “Daily Reconciliation Summary”  
**Body (HTML Format):**
```html
<h3>Finance Reconciliation Summary</h3>
<p><strong>Matched:</strong> 17</p>
<p><strong>Not Found:</strong> 3</p>
<p>Unmatched transactions require review. Please check the attached sheet.</p>

## 🔗 Related Post

I shared a detailed breakdown of this automation project and its real-world impact on finance teams on LinkedIn.  
➡️ [View the full post on LinkedIn](https://www.linkedin.com/posts/basitalidiyal_automation-ai-n8n-activity-7385236032289505280-Ee7r)

---

