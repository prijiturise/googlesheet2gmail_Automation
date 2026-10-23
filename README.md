# Google Sheets to Gmail Email Automation using n8n

## 1. Project Overview

This project automates the process of reading student records from Google Sheets, formatting the data into a structured email, and sending the email through Gmail using n8n.

The workflow eliminates manual email preparation by dynamically generating an email subject and message body from spreadsheet data.

**Project:** Google Sheets to Gmail Email Automation  
**Difficulty:** Beginner to Medium  
**Platform:** n8n Cloud  
**Language:** JavaScript

## 2. Problem Statement

Manually collecting data from spreadsheets and composing emails can be time-consuming and repetitive.

The objective of this project is to build an n8n workflow that reads student information from Google Sheets, transforms it into a clean and readable email, and sends it to a chosen email address through Gmail.

The workflow must also handle empty data gracefully without sending a blank email.

## 3. Technologies Used

- **n8n Cloud:** Workflow automation platform.
- **Google Sheets:** Stores student records.
- **JavaScript Code Node:** Formats records and generates the email subject and body.
- **Gmail:** Sends the generated email.
- **Google OAuth2:** Authenticates access to Google Sheets and Gmail.

## 4. Workflow Architecture

The workflow consists of four nodes:

1. **Manual Trigger** — Starts the workflow when executed manually.
2. **Google Sheets — Get Row(s)** — Retrieves student records from the spreadsheet.
3. **Code** — Processes the records and creates the email subject and body.
4. **Gmail — Send a message** — Sends the formatted email to the configured recipient.

**Workflow sequence:**

`Manual Trigger → Google Sheets → Code → Gmail`

## 5. Google Sheets Structure

The Google spreadsheet is named `Student Records`, and the worksheet is named `Students`.

| Name | Course | Status |
|---|---|---|
| Arun | Python | Completed |
| Priya | AI and ML | In Progress |
| Kavin | Data Analytics | Pending |

The first row contains the column headers used by the Code node.

## 6. Email Generation

The Code node reads the student records and creates a structured email.

### Subject generation

- If all students share the same status, the subject includes that status.
- If students have different statuses, the subject is `Student Status Report - Multiple Statuses`.

### Email body

The email includes:
- A greeting.
- The list of student names.
- Each student's course and status.
- The total number of students.
- A closing message from the automation bot.

### Sample email

**Subject:** Student Status Report - Multiple Statuses

Hello,

Please find below the latest student status report.

1. Arun  
   Course: Python  
   Status: Completed

2. Priya  
   Course: AI and ML  
   Status: In Progress

3. Kavin  
   Course: Data Analytics  
   Status: Pending

Total students: 3

Regards,  
Your Automation Bot

## 7. Empty Data Handling

The Code node filters out records that do not contain a name, course, or status.

If no valid records remain, it returns an empty array. Consequently, the Gmail node does not receive an item to send.

This prevents the workflow from generating a blank email when the sheet contains no valid student records.

## 8. Implementation Steps

1. Create a Google spreadsheet named `Student Records`.
2. Add the columns `Name`, `Course`, and `Status`.
3. Create a new workflow in n8n Cloud.
4. Add a Manual Trigger node.
5. Add a Google Sheets node and configure the Get Row(s) operation.
6. Connect the Google account and select the `Students` worksheet.
7. Add a Code node and paste the JavaScript email-generation code.
8. Add a Gmail node and configure the Send operation.
9. Set the recipient's email address.
10. Configure the subject using `{{ $json.subject }}`.
11. Configure the message body using `{{ $json.body }}`.
12. Execute the workflow and verify the email in the recipient's inbox.

## 9. Testing and Validation

The following scenarios should be tested:

- **Normal execution:** All student records are retrieved and included in the email.
- **Subject generation:** The subject reflects the students' status information.
- **Readable formatting:** The email displays structured student details instead of raw JSON.
- **Empty sheet:** No email is sent when there are no valid records.
- **Gmail delivery:** The email reaches the configured recipient.
- **Credential validation:** Both Google Sheets and Gmail connections work successfully.

## 10. Security Considerations

- Store Google credentials securely using n8n credentials.
- Do not hardcode passwords, access tokens, or API secrets in the Code node.
- Use a test email address during development.
- Grant only the permissions required by the workflow.

## 11. Future Enhancements

The workflow can be extended to:

- Run automatically using a Schedule Trigger.
- Generate separate emails for different student statuses.
- Include status-wise student counts in the subject.
- Send HTML-formatted emails with tables.
- Add error handling and execution notifications.
- Filter records based on course or status.

## 12. Conclusion

This project demonstrates how n8n can integrate Google Sheets and Gmail to automate data processing and email delivery.

It combines data retrieval, JavaScript transformation, and email delivery into a single workflow, reducing repetitive manual work and producing consistent, readable email reports.

The project also demonstrates basic data validation and empty-data handling, making the automation more reliable.
