# Copperfox Gov Sync PAPI  

## Overview  

The `copperfox-gov-sync-papi` is an API hosted on MuleSoft Gov Cloud. It processes Salesforce ContentDocuments for a given record ID by consolidating CSV files into a single file. If the consolidated file size is less than 10MB, it replaces all existing files on the parent record with the new file in Salesforce. If the file size is 10MB or more, a notification email is sent.  

## Project Structure  

### 1. Flow Components  

The flow performs the following actions:

1. **Validate Subscriber Key**  
   - The flow first validates the provided subscriber key by querying Salesforce to check if the user is active. If invalid, an error is raised (`SFAPP:INVALID_USER`).

2. **Retrieve Files**  
   - After successful key validation, the flow queries Salesforce for all `ContentDocumentId`s associated with the given Salesforce record ID.

3. **File Validation and Consolidation**  
   - The flow checks if the attached files are CSV format and calculates the total size of the files. If valid, it consolidates the contents of all CSV files (excluding headers) into a single file.

4. **File Upload to Salesforce**  
   - If the total size of the consolidated file is under 10MB, it uploads the file to Salesforce as a new `ContentVersion`, replacing any existing files on the record. 
   - If the file size exceeds 10MB, no upload occurs, and a failure response is sent through mail.

5. **Notifications**  
   - Success or failure notifications are triggered after each key step, including after uploading the consolidated file or if the file size exceeds the limit. 

### 2. Error Handling  

- If any validation fails (e.g., invalid subscriber key, non-CSV files, file size exceeds limits), an error is logged, and an email notification is sent.
- If the file is successfully uploaded to Salesforce, an email notification is sent.

## Setup  

### Prerequisites  

- Mule Runtime  
- Salesforce Account 
- Valid subscriber keys  
- Email SMTP configuration for notifications  
