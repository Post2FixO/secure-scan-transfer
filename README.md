# secure-scan-transfer

Easy and secure direct scanning to remote folders.

## Intro

**secure-scan-transfer** is a PowerShell script that secures scanning from cloud enabled shared scanners to workstations or servers. Desktop clients can be used to sync scans to a computer but copies of the scans can remain accessible on shared scanners and in cloud storage. This script actively monitors cloud-synced folders, moving incoming files to local folders, automatically deleting scans from cloud storage and therefore from the shared scanner interfaces in public areas like shared office spaces.

The ability to use cloud integrations that are encrypted by default eliminates the need to rely on outdated, less secure protocols such as SMB or FTP, which often require additional security layers like VPNs that can still expose files on local networks. **secure-scan-transfer** allows admins to easily setup advanced and secure direct scanning to remote folders.

## Running the Script

To start the script, open PowerShell and run the following command:

```powershell
powershell -ExecutionPolicy Bypass -File "path_to_your_script.ps1"
```

This method (`-ExecutionPolicy Bypass`) allows the script to run without changing the global execution policy permanently. It bypasses the policy only for the current session, ensuring that your script can execute while maintaining stricter security policies by default.

## Setup Instructions

### Prerequisites

- Windows OS with PowerShell.
- Read/write access to the specified source and destination directories.
- Cloud sync client installed (e.g., Google Drive for Desktop, Dropbox).

### Configuration Steps

1. **Set the User Account**: Specify the username of the account on the local machine where files will be moved.

    ```powershell
    $user = "your_username"
    ```

2. **Select Your Cloud Service**: Uncomment the line corresponding to the cloud service where your scanner uploads documents.

    ```powershell
    $service = "My Drive"  # For Google Drive for Desktop
    #$service = "DropBox"  # Uncomment if using Dropbox
    ```

3. **Define Source and Destination Folders**: Replace `<source folder>` and `<destination folder>` with the actual folder names where your scanner uploads files and where you want them to be moved.

    ```powershell
    $folderPairs = @(
        @{ Source = "C:\Users\$user\$service\<source folder>"; Destination = "C:\Users\$user\<destination folder>" },
    )
    ```

4. **Add Additional Folder Pairs** as needed by copying the line in the `$folderPairs` array and adjusting the paths accordingly.

## Usage Notes

- **Monitoring**: Once started, the script will continuously monitor the specified source folders and move new files to the designated folders, showing activity logs.
- **Management**: The PowerShell terminal can be minimized but should remain running in the background to maintain functionality (intil further integration).
- **Stopping the Script**: To stop the script, press `Ctrl+C` in the PowerShell window.
