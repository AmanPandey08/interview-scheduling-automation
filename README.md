# Interview Scheduling Automation

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
- Airtable (Base, Tables, Formula Fields)
- Airtable Scripting Extension
- MailerSend API
- CSV Dataset

---

## Workflow
1. Import candidate data from CSV into Airtable
2. Split multiple interview rounds into separate rows
3. Validate candidate email addresses
4. Send interview invitation emails with Calendly links
5. Update mail status and timestamps
6. Calculate turnaround time (TAT)

---

## Features
- Handles candidates with multiple interview rounds
- Automated email communication
- Email validation and error handling
- Accurate TAT calculation
- Free-tier friendly implementation

---

## Data Processing
- Candidates with multiple interview rounds are split into separate records
- Each record contains one interview round and its corresponding Calendly link
- Original candidate information remains unchanged across split rows

---

## Email Automation
- Emails are sent using the MailerSend API
- Records are marked as:
  - Sent
  - Pending
  - Failed
  - Invalid Email
- Invalid email domains are skipped gracefully to avoid API failures

---

## Turnaround Time (TAT)
TAT is calculated using the formula:
  Calculate TAT = Mail Sent Time - Added On Time.


TAT is calculated only for successfully sent emails to ensure accuracy and avoid misleading metrics for failed or invalid email records.

---

## Edge Cases Handled
- Candidates with multiple interview rounds in a single row
- Invalid or malformed email addresses
- API call failures and retries
- Duplicate email prevention using mail status checks
- Accurate timestamp-based TAT calculation

---

## Assumptions
- Each interview round contains a single Calendly link
- Email delivery success is determined by the MailerSend API response
- Invalid email domains are expected in the dataset and handled gracefully
- Free-tier limitations of Airtable are acceptable for this implementation

---

## Conclusion
This project demonstrates a practical, production-style automation workflow that streamlines interview scheduling and communication. It focuses on data integrity, error handling, and accurate turnaround time tracking while working within real-world platform constraints.

---

## Author
Aman Pandey


