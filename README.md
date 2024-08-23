
### `health-ehr-inventory-api-flow`

## Overview

The `health-ehr-inventory-api-flow` is part of a Mule application that integrates a generic Inventory Management System (Inventory) with an Electronic Health Record (EHR). This flow runs daily at 9:00 PM EST to retrieve inventory data from a cloud-based relational database and send it to the EHR in JSON format. The flow is designed to handle and log errors efficiently, including retrying failed connections and notifying stakeholders via email.

### Flow Components and Description:

1. **Scheduler:**
   - Triggers the flow daily at 9:00 PM EST.

2. **Start Logger:**
   - Logs the start time and flow name.

3. **Database Query:**
   - Retrieves data from the database.
   - Logs the number of records retrieved.
   - Handles errors:
     - Retries connections on connectivity issues with a set retry count.
     - Logs other errors immediately.
     - Sends error notifications via email to ensure prompt response and recovery.

4. **Data Transformation:**
   - Converts the retrieved data into JSON format for the EHR.

5. **HTTP Request to EHR:**
   - Sends the JSON data to the EHR via a POST request.
   - Handles errors:
     - Retries on connectivity issues with a set retry count.
     - Logs other errors immediately.
     - Sends error notifications via email to ensure prompt response and recovery.

6. **End Logger:**
   - Logs the end time and flow name.
