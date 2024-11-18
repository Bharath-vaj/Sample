# Copperfox Gov Sync PAPI  

## Overview  

The `copperfox-gov-sync-papi` is an API hosted on MuleSoft Gov Cloud. It processes Salesforce ContentDocuments for a given record ID by consolidating CSV files into a single file. If the consolidated file size is less than 10MB, it replaces all existing files on the parent record with the new file in Salesforce. If the file size is 10MB or more, a notification email is sent.  

## Project Structure  

### 1. Flow Components  

1. **HTTP Listener**: Accepts incoming requests.  
2. **Subscriber Key Validation**: Validates the provided subscriber key.  
3. **Salesforce Connection**: Retrieves ContentDocuments and Versions for the record ID.  
4. **File Type Validation**: Processes only `.csv` files.  
5. **CSV Consolidation**: Combines CSV contents, excluding duplicate headers.  
6. **File Management**:  
   - Replaces existing files in Salesforce if the consolidated file size is < 10MB.  
   - Sends a notification email if the consolidated file size is ≥ 10MB.  

### 2. Error Handling  

- Invalid key or file type: Logged and returned as an error.  
- Salesforce connection or size errors: Logged and notified via email.  

## Setup  

### Prerequisites  

- Mule Runtime  
- Salesforce Account 
- Valid subscriber keys  
- Email SMTP configuration for notifications  
