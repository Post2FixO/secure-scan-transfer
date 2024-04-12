# secure-scan-transfer

**Easy and secure scanning from public scanners to remote file systems.**

## Introduction

"**secure-scan-transfer** is a PowerShell script that enhances security when scanning documents from public office space scanners directly to internet-connected workstations or servers. While cloud sync desktop clients offer a straightforward way to transfer scans to computers, copies can remain accessible on shared scanners and in cloud storage. This script proactively monitors cloud-synced folders, moving any incoming files to local directories and automatically deleting scans from both cloud storage and the publicly accessible interfaces of shared scanners.

Cloud scanner integrations provide encryption by default, which avoids reliance on outdated and less secure scanner protocols like SMB or FTP. These protocols often require additional security measures such as site-to-site VPNs, which are complex to configure and can still inadvertently expose files on local networks. **secure-scan-transfer** simplifies the setup for administrators, offering an advanced, secure, and user-friendly solution for direct scanning to remote computers."

## Running the Script

To launch the script, open PowerShell and execute the following command:

```powershell
powershell -ExecutionPolicy Bypass -File "<path_to_your_script>\secure-scan-transfer.ps1"
```

Using `-ExecutionPolicy Bypass` allows the script to run without permanently changing the global execution policy. This method bypasses the policy only for the current session, ensuring that the script executes while maintaining stricter security policies by default.

## Setup Instructions

### Prerequisites

- A Windows operating system with PowerShell.
- Read/write access to the specified source and destination directories.
- A cloud sync client installed (e.g., Google Drive for Desktop, Dropbox).

### Configuration Steps

1. **Set the User Account**:
   Define the username of the account on the local machine where files will be moved.

    ```powershell
    $user = "your_username"
    ```

2. **Select Your Cloud Service**:
   Choose the cloud service where your scanner uploads documents. Uncomment the appropriate line.

    ```powershell
    $service = "My Drive"  # For Google Drive for Desktop
    #$service = "DropBox"  # Uncomment if using Dropbox
    ```

3. **Define Source and Destination Folders**:
   Replace `<source folder>` and `<destination folder>` with the actual folder names where scans are uploaded and where you wish to move them.

    ```powershell
    $folderPairs = @(
        @{ Source = "C:\Users\$user\$service\<source folder>"; Destination = "C:\Users\$user\<destination folder>" },
    )
    ```

4. **Add Additional Folder Pairs**:
   Extend functionality by adding more folder pairs to the `$folderPairs` array as needed.

## Usage Notes

- **Monitoring**: The script will continuously monitor specified source folders and relocate new files to the designated destinations, displaying activity logs.
- **Management**: Minimize the PowerShell terminal to run the script in the background. Ensure it remains active to maintain functionality.
- **Stopping the Script**: Press `Ctrl+C` in the PowerShell window to terminate the script.
