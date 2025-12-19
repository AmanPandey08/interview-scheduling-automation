# Weekday – Interview Scheduling Automation  
**YC W21 | Founder’s Office Coding Assignment**

An automated workflow to streamline interview scheduling, candidate communication, and turnaround time (TAT) tracking using Airtable and MailerSend.

## Overview
This project automates the process of handling interview scheduling by:
- Cleaning and restructuring candidate data
- Splitting multiple interview rounds into individual records
- Sending interview invitation emails with appropriate Calendly links
- Calculating turnaround time (TAT) for the scheduling process

The solution is built using Airtable’s scripting capabilities and the MailerSend email API, while remaining compatible with free-tier tool limitations.

---

## Tech Stack
- **Airtable** – Data storage and scripting
- **Airtable Scripting Extension** – Data processing and automation
- **MailerSend API** – Email delivery
- **CSV Dataset** – Candidate interview data

---

## Workflow
1. Import candidate data from CSV into Airtable
2. Split multiple interview rounds into separate rows
3. Validate candidate email addresses
4. Send interview invitation emails with Calendly links
5. Update mail status and timestamps
6. Calculate turnaround time (TAT)
<img width="1618" height="767" alt="image" src="https://github.com/user-attachments/assets/122cb152-8617-4ddb-8dfc-45075cc10acb" />
---

## Task 1: Data Splitting

### Problem
Some candidates have multiple interview rounds stored in a single cell under the **Scheduling method** column.
 <img width="1007" height="513" alt="image" src="https://github.com/user-attachments/assets/f550a74c-846c-4097-a84b-4d949af341e4" />
 
---

### Solution
- Imported the CSV into Airtable as `Candidates_Raw`
  <img width="1917" height="917" alt="image" src="https://github.com/user-attachments/assets/be693481-bbd7-4e1f-9f96-dafc12d08e87" />
- Created a new table `Candidates_Split`
  <img width="1918" height="910" alt="image" src="https://github.com/user-attachments/assets/437adb56-cee0-47d1-861e-7c0f8e012c58" />
- Used Airtable Scripting to:
  - Parse interview rounds line by line
  - Extract interview round names and Calendly links
  - Create one row per interview round
    <img width="1487" height="705" alt="image" src="https://github.com/user-attachments/assets/1b585191-b6a0-4f0a-a399-5c1de858c6f4" />

### Result
If a candidate has **3 interview rounds**, **3 separate rows** are created with the same candidate details and different interview rounds and Calendly links.

---

## Task 2: MailerSend Integration
 ### MailerSend API to send interview invitation emails
  <img width="1537" height="790" alt="image" src="https://github.com/user-attachments/assets/10e45112-a53c-4c94-aa15-3fe2da1fd0b9" />

### Problem
- Airtable free tier does not support **Run Script** inside Automations
- Browser-based scripts face **CORS limitations**

### Solution
- Used **Airtable Scripting Extension**
- Used `remoteFetchAsync()` to bypass CORS
- Implemented a master email script that:
  - Identifies records with `Mail Status = Pending`
  - Sends interview invitation emails using MailerSend
  - Updates mail status based on API response

### Email Logic
- **Valid email** → Email sent → Status marked as **Sent**
- **Invalid email domain** → Skipped → Status marked as **Invalid Email**
- **API rejection** → Status marked as **Failed**
  <img width="504" height="572" alt="image" src="https://github.com/user-attachments/assets/9aca1a94-cfaf-40e5-87a2-6ae18b84e232" />


📌 **Note:** The dataset intentionally includes invalid email domains (e.g., `gmail1234.com`) to test validation and error handling.
<img width="1916" height="913" alt="image" src="https://github.com/user-attachments/assets/effca72e-c89d-43cd-a497-0d1c4a8d4ac3" />
---

## Task 3: TAT (Turnaround Time) Calculation

### Fields Used
- **Added On** – Timestamp from the original dataset
- **Mail Sent Time** – Updated only when an email is successfully sent
- **TAT (Minutes)** – Formula field

### Formula Used
  DATETIME_DIFF({Mail Sent Time}, {Added On}, 'minutes')

-This is an Airtable formula to calculate TAT (Turn Around Time) in minutes between when the candidate was added and when the mail was sent.
-TAT is calculated only for successfully sent emails to ensure accuracy and avoid misleading metrics for failed or invalid email records.

---

## Edge Cases Handled
- Candidates with multiple interview rounds in a single row
- Invalid or malformed email addresses
- API call failures and retries
- Duplicate email prevention using mail status checks
- Accurate timestamp-based TAT calculation

---

## Conclusion
This project demonstrates a practical, production-style automation workflow that streamlines interview scheduling and communication. It focuses on data integrity, error handling, and accurate turnaround time tracking while working within real-world platform constraints.

---

## Author
Aman Pandey


