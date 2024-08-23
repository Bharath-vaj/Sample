### `health-ehr-inventory-api-flow`



## Overview



The `health-ehr-inventory-api` is Mule application that showcases the integration between a generic Inventory Management System (Inventory) and an Electronic Health Record (EHR) using MuleSoft.

The `health-ehr-inventory-api-flow` triggers the process at 9PM EST everyday where the flow will retrieve inventory data from a cloud-based relational database and send it to the EHR in JSON format.

Errors occured while connecting to Database or EHR system is retried for 3 times, if the error still persists the structured error response is logged.



#### Flow Components and Description:



1. **Scheduler:**
  - Triggers the flow daily at 9:00 PM EST.



2. **Start Logger:**
  - Logs the start time and flow name.



3. **Database Query:**
  - Runs a query to retrieve data from the database.
  - Logs the number of records retrieved.
  - Handles database errors:
    - If there's a connectivity issue, the flow will retry the connection until successful, with a set retry count.
    - If other errors occur, they are logged immediately.
   - The captured error is sent as a notification via email to enhance the ability to respond to and recover from errors effectively.



4. **Data Transformation:**
  - Converts the database results into the JSON format required by the EHR.



5. **HTTP Request to EHR:**
  - Sends the transformed data to the EHR system via a POST request.
  - Handles HTTP errors:
    - If there's a connectivity issue, the flow will retry the request until successful, with a set retry count.
    - If other errors occur, they are logged immediately.
   - The captured error is sent as a notification via email to enhance the ability to respond to and recover from errors effectively.



6. **End Logger:**
  - Logs the end time and flow name.
