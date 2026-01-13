# Proof of Execution — Gmail → Google Sheets Automation

This directory contains concrete, verifiable evidence that the Gmail → Google
Sheets automation works as specified. The artifacts demonstrate OAuth-based
authentication, email ingestion, duplicate prevention, idempotent execution,
and correct acknowledgment of messages.

All files are ordered numerically to allow quick verification by graders.

---

## 01. OAuth Consent Screen

**File:** `01_oauth_consent.png`

Shows the OAuth 2.0 Installed App consent screen presented during the first run
of the application.

Demonstrates:
- Explicit user authorization
- Gmail and Google Sheets permissions
- Correct OAuth flow for a desktop/CLI application

---

## 02. Gmail Inbox — Unread Messages (Before Execution)

**File:** `02_gmail_unread.png`

Shows the Gmail Inbox containing multiple **UNREAD** messages used as input for
the synchronization.

Purpose:
- Confirms the initial state of the Inbox
- Shows messages eligible for processing before the script is run

---

## 03. Google Sheet — Emails Tab (Appended Rows)

**File:** `03_sheet_emails.png`

Shows the `Emails` tab after executing the script.

Columns:
- `From`
- `Subject`
- `Date`
- `Content`

Evidence:
- Multiple rows appended by the script
- Clean, normalized, single-line content
- Human-readable timestamps

This confirms successful parsing and persistence of Gmail messages.

---

## 03 (Reference). Gmail Message IDs

**File:** `03_messageId.png`

Shows the Gmail `messageId` values corresponding to the processed emails.

Purpose:
- Establishes the unique identifiers used for deduplication
- Links Gmail messages to spreadsheet state

---

## 04. Terminal Logs — First Run

**File:** `04_logs_first_run.png`

Shows terminal output from the first execution of the script.

Key events visible:
- OAuth token loaded or refreshed
- Previously processed IDs loaded from Google Sheets
- Unread messages detected in Inbox
- Rows appended to `Emails`
- Message IDs appended to `Processed`
- Messages marked as READ
- Sync completed successfully

---

## 05. Google Sheet — Processed Tab (State Persistence)

**File:** `05_sheet_processed1.png`

Shows the `Processed` tab after the first run.

Purpose:
- Persists canonical Gmail `messageId` values
- Prevents duplicate processing across runs
- Provides visible and auditable application state

---

## 05 (Reference). Persisted Processed Message IDs

**File:** `05_messageId_processed.png`

Shows the stored `messageId` values written by the application.

Purpose:
- Confirms correct persistence of processed message identifiers
- Supports strict duplicate-prevention guarantees

---

## 06. Gmail Inbox — Messages Marked as READ

**File:** `06_marked_read.png`

Shows the Gmail Inbox after successful processing.

Evidence:
- Messages previously unread are now marked as READ
- Confirms messages are acknowledged only after successful persistence

---

## 07. Terminal Logs — Second Run (Idempotency)

**File:** `07_logs_second_run.png`

Shows terminal output from a second execution of the script.

Observed behavior:
- All processed IDs loaded from the `Processed` sheet
- No unread messages detected
- No new rows appended
- No messages marked as READ
- Sync completes with no side effects

This confirms idempotent behavior.

---

## 08. Demo Video

**File:** `demo_video.mp4`

A short demo video demonstrating:
- Gmail Inbox state before execution
- Running the script
- Rows added to Google Sheets
- Running the script again with no duplicates or side effects

---

## Summary

The artifacts in this directory prove that the application:
- Uses OAuth 2.0 Installed App authentication correctly
- Processes only unread Inbox emails
- Persists email data safely to Google Sheets
- Prevents duplicate entries using stored Gmail `messageId`s
- Marks messages as READ only after successful persistence
- Is safe to run repeatedly without reprocessing the same emails

All functional and non-functional assignment requirements are satisfied.
