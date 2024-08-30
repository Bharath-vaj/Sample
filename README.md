
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
  
# Installation and Setup Guide

## 1. Install curl using Chocolatey

### Step 1: Install Chocolatey
Open PowerShell as Administrator:
1. Click on the Start menu, type PowerShell, right-click on Windows PowerShell, and select Run as administrator.
2. Run the following command to install Chocolatey:
   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
   ```

### Step 2: Verify Chocolatey Installation
Close and reopen PowerShell as Administrator.
Run the following command to check if Chocolatey is installed:
```powershell
choco
```

### Step 3: Install curl using Chocolatey
Run the following command in PowerShell:
```powershell
choco install curl -y
```

### Step 4: Verify curl Installation
Check if curl is installed:
Open Command Prompt or PowerShell and run:
```powershell
curl --version
```

## 2. Clone the Repository and Download the File

### Step 1: Navigate to the Desired Directory
Use the command line to navigate to the directory where you want to clone the repository.

### Step 2: Clone the Repository
Run the following command:
```bash
git clone https://github.com/mulesoft-labs/data-weave-cli.git
```

### Step 3: Download the CLI
Run the following command:
```bash
curl -L -o dataweave-cli.zip "https://github.com/mulesoft-labs/data-weave-cli/releases/download/v1.0.34/dw-1.0.34-Windows"
```

### Step 4: Unzip the File using 7-Zip
Run the following command:
```bash
"C:\Program Files\7-Zip\7z.exe" x "C:\Users\Nishanthi\dataweave-cli\dataweave-cli.zip" -o%USERPROFILE%\.dw
```

### Step 5: Add DataWeave CLI to PATH
Run the following command:
```bash
setx PATH "%PATH%;%USERPROFILE%\.dw\bin"
```

### Step 6: Verify DataWeave CLI Installation
Run the following command:
```bash
dw --version
```

## 3. Install JDK-17

### Step 1: Download JDK-17
Run the following command:
```bash
curl -L -o jdk-17.zip https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.12%2B7/OpenJDK17U-jdk_x64_windows_hotspot_17.0.12_7.zip
```

### Step 2: Unzip the File using 7-Zip
Run the following command:
```bash
"C:\Program Files\7-Zip\7z.exe" x jdk-17.zip -o%USERPROFILE%\jdk-17
```

### Step 3: Set Path
Run the following commands:
```bash
setx PATH "%PATH%;%USERPROFILE%\jdk-17\bin"
setx JAVA_HOME "%USERPROFILE%\jdk-17"
```

## 4. Install GraalVM

### Step 1: Download GraalVM
Run the following command:
```bash
curl -L -o graalvm.zip https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-17.0.8/graalvm-community-jdk-17.0.8_windows-x64_bin.zip
```

### Step 2: Unzip the File using 7-Zip
Run the following command:
```bash
"C:\Program Files\7-Zip\7z.exe" x graalvm.zip -o%USERPROFILE%
```

### Step 3: Set JAVA_HOME and GraalVM_HOME
Set the environment variables for GraalVM.

## 5. Install Visual Studio Build Tools

### Step 1: Install Visual Studio Build Tools
During installation, make sure to include Desktop development with C++ and Windows SDK.

### Step 2: Set Path
Set the path as:
```bash
C:\Program Files\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build
```

## 6. Compile the Project

### Step 1: Navigate to Project Location
Use the command line to navigate to the project location.

### Step 2: Execute the Command
Run the following command:
```bash
gradlew native-cli:nativeCompile
```

## 7. Run the Command

### Step 1: Execute the Command
Run the following command:
```bash
dw run -i payload=<fullpathToUsers.json>  "output application/json ---payload map (value, index) -> { (index) : value}"
```

