# Webhook CRM Lead Automation

An end-to-end lead automation system built with n8n, Supabase, HubSpot CRM, and Telegram.

## Overview

This project automates the process of receiving a real-estate lead, validating the data, checking for duplicate leads, storing the lead in Supabase, syncing the lead with HubSpot CRM, notifying the sales team through Telegram, and recording workflow execution logs.

## Problem

Real-estate businesses may receive many leads from forms or other sources.

Manually processing these leads can cause:

- Slow lead processing
- Duplicate records
- Data entry mistakes
- Delayed sales-team notifications
- Missed follow-ups

## Solution

This automation handles the lead-processing workflow automatically.

A lead enters through a webhook and is processed through validation, duplicate checking, database storage, CRM synchronization, notification, and logging.

## Workflow Architecture

Postman / Website Form
        ↓
Receive Lead
        ↓
Normalize Lead Data
        ↓
Check Existing Lead
        ↓
Find Lead in Database
        ↓
Lead Exists?
        ↓
Save New Lead
        ↓
Sync Lead to HubSpot
        ↓
Notify Sales Team
        ↓
Prepare Log Data
        ↓
Save Execution Log

## Technologies Used

- n8n
- Supabase
- HubSpot CRM
- Telegram Bot
- Postman
- REST API
- Webhooks
- JavaScript
- JSON

## Workflow Steps

### 1. Receive Lead

A webhook receives lead information such as:

- Name
- Email
- Phone
- Property
- Message

### 2. Normalize Lead Data

The incoming webhook data is cleaned and structured into a consistent format for the rest of the workflow.

### 3. Check Existing Lead

The workflow checks whether the incoming lead already exists in the database.

### 4. Find Lead in Database

Supabase is queried to find an existing lead using the lead email.

### 5. Lead Exists?

An IF condition determines whether the lead already exists.

- If the lead exists, the workflow prevents creating a duplicate lead.
- If the lead does not exist, a new lead record is created.

### 6. Save New Lead

New lead information is stored in the Supabase database.

Example:

Name: John Doe  
Email: john@gmail.com  
Phone: +123456789  
Property: 3 Bedroom Apartment  
Message: I'm interested in this property.

### 7. Sync Lead to HubSpot

The lead is created or updated as a contact in HubSpot CRM.

### 8. Notify Sales Team

After the CRM operation, Telegram sends a notification containing the lead details.

Example:

🚨 New Lead Received!

Name: John Doe  
Email: john@gmail.com  
Phone: +123456789  
Property: 3 Bedroom Apartment

Please follow up with the lead.

### 9. Prepare Log Data

JavaScript is used to prepare workflow execution information for logging.

The log contains information such as:

- Run ID
- Status
- Records received
- Records created
- Records failed
- Error message
- Start time
- Completion time

### 10. Save Execution Log

The execution information is stored in a dedicated Supabase logging table.

This allows workflow executions to be tracked and failures to be investigated.

## Duplicate Protection

The workflow checks the lead email before creating a new database record.

This helps prevent duplicate lead records.

## Error Handling

The workflow uses conditional logic to handle existing and new leads.

The HubSpot operation is also configured to provide an error path so that CRM/API failures can be handled.

## End-to-End Testing

The complete workflow was tested using Postman because a production website or frontend form was not required for this project.

Test flow:

Postman
→ Webhook
→ Validation
→ Duplicate Check
→ Supabase
→ HubSpot
→ Telegram
→ Logging

## Result

The test lead successfully passed through the automation workflow.

The lead was:

- Received through the webhook
- Stored in Supabase
- Created or updated in HubSpot
- Sent to Telegram
- Recorded in the workflow logs

## Project Structure

project-2-webhook-crm-automation/

├── README.md  
├── workflow.json  
└── screenshots/

## Purpose

This project demonstrates a practical business process automation system using n8n and multiple external services.

It shows how a lead management process can be automated from lead collection to database storage, CRM synchronization, team notification, and workflow logging.

## Future Improvements

- Real website form integration
- Email notifications
- AI-based lead qualification
- Lead scoring
- CRM deal creation
- Retry mechanisms
- Advanced monitoring
- Production security configuration